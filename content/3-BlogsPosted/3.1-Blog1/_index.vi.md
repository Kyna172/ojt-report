---
title: "Blog 1"
date: 2025-08-11
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Bảo mật đặc quyền tối thiểu với Amazon EKS Pod Identity và Session Policies

### Mở đầu & Bối cảnh bài toán
Khi triển khai các ứng dụng container hóa trên Kubernetes bằng dịch vụ Amazon EKS, việc cấp quyền AWS cho các Pod luôn là một bài toán khiến nhiều kỹ sư đau đầu. Trước đây, cộng đồng thường dùng giải pháp **IAM Roles for Service Accounts (IRSA)**. Dù IRSA rất mạnh nhưng lại đòi hỏi phải thiết lập nhà cung cấp định danh OIDC (OpenID Connect) và cấu hình Trust Policy tương đối phức tạp cho từng cụm cluster.

Mới đây, AWS đã tung ra **Amazon EKS Pod Identity**, giúp đơn giản hóa việc gắn quyền cho Pod chỉ thông qua một DaemonSet agent cài sẵn trên EKS. Đặc biệt hơn, tính năng **Session Policies** đi kèm cho phép chúng ta thu hẹp quyền hạn của từng Pod một cách cực kỳ linh hoạt mà không cần phải tạo ra cả trăm IAM Role rời rạc.

---

### Tại sao Session Policies lại là một bước tiến lớn?
Trong môi trường microservices có hàng chục dịch vụ chạy chung:
1. **Tránh bùng nổ số lượng IAM Role:** Giả sử Pod A chỉ cần đọc bucket `bao-cao-tai-chinh`, còn Pod B chỉ cần đọc bucket `du-lieu-marketing`. Trước đây, anh em DevOps bắt buộc phải tạo 2 IAM Role riêng biệt. Càng nhiều dịch vụ thì số lượng role càng tăng chóng mặt.
2. **Không lo chạm giới hạn Quota:** Mỗi tài khoản AWS có giới hạn số lượng IAM Role (mặc định khoảng 1.000 role). Với các cụm Kubernetes lớn, việc tạo role cho từng pod rất dễ chạm trần quota.
3. **Nguyên lý giao thoa quyền hạn (Intersection):** Quyền thực tế mà Pod nhận được chính là **phần giao** giữa quyền của IAM Role gốc và quyền trong Session Policy:

$$\text{Quyền thực tế} = \text{Quyền của IAM Role} \cap \text{Quyền trong Session Policy}$$

> **Lưu ý cốt lõi:** Session Policy chỉ có tác dụng **thu hẹp (narrow)** quyền hạn, chứ tuyệt đối không bao giờ mở rộng thêm quyền vượt quá quyền của IAM Role gốc.

---

### Cơ chế hoạt động thực tế

1. Pod trong Kubernetes được khởi chạy kèm theo một ServiceAccount được chỉ định.
2. EKS Pod Identity Agent (chạy dạng DaemonSet trên từng worker node) sẽ đón bắt các cuộc gọi lấy chứng chỉ từ AWS SDK bên trong container.
3. EKS gửi yêu cầu tới AWS STS để xin cấp chứng chỉ tạm thời cho IAM Role tương ứng, kèm theo chính sách **Session Policy** đã được khai báo.
4. Pod nhận được bộ khóa tạm thời (Access Key, Secret Key, Session Token) và chỉ thực hiện được đúng các quyền hạn đã được siết chặt.

---

### Ví dụ cấu hình thực tế

#### 1. Tạo IAM Role gốc (Base Role)
Giả sử ta tạo một Role dùng chung cho việc đọc S3 mang tên `EKS-General-Storage-Role`:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": "*"
    }
  ]
}
```

#### 2. Giới hạn riêng cho từng Pod bằng Session Policy
Khi liên kết ServiceAccount với IAM Role qua câu lệnh AWS CLI, ta truyền thêm Session Policy chỉ cho phép Pod của dịch vụ tài chính đọc đúng bucket `my-finance-reports-prod`:

```bash
aws eks create-pod-identity-association \
  --cluster-name production-eks-cluster \
  --namespace finance-apps \
  --service-account finance-reporter \
  --role-arn arn:aws:iam::123456789012:role/EKS-General-Storage-Role \
  --client-token $(uuidgen)
```

Nội dung Session Policy thu hẹp:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::my-finance-reports-prod/*"
    }
  ]
}
```

Dù IAM Role gốc cho phép đọc mọi bucket S3, nhưng Pod tài chính này khi chạy thực tế chỉ có thể đọc dữ liệu trong bucket `my-finance-reports-prod`, nếu cố tình truy cập sang bucket khác sẽ lập tức nhận lỗi `AccessDenied`.

---

### Lời khuyên khi áp dụng vào thực tế
* **Quản trị tập trung:** Hãy nhóm các dịch vụ có mục đích tương tự nhau vào một Base Role, sau đó dùng Session Policy để tinh chỉnh chi tiết cho từng môi trường (Dev, Staging, Prod).
* **Đơn giản hóa hạ tầng:** Bỏ bớt sự phụ thuộc vào OIDC Provider URL giúp mã nguồn Terraform/CloudFormation tạo cụm EKS ngắn gọn và ít lỗi phụ thuộc hơn rất nhiều.
* **Minh bạch khi kiểm toán:** Lịch sử gọi lệnh trên AWS CloudTrail hiển thị rõ cả tên Role và Session Name, giúp đội ngũ bảo mật dễ dàng tra cứu khi có sự cố.
