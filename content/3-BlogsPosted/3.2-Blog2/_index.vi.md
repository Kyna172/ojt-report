---
title: "Blog 2"
date: 2025-08-11
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Tối ưu hiệu năng và bảo mật lưu trữ Web tĩnh với S3 và CloudFront OAC

### Bài toán: Vừa muốn web chạy nhanh, giá rẻ, vừa phải tuyệt đối an toàn
Khi làm đồ án hoặc triển khai các ứng dụng Frontend hiện đại (React, Vue, Angular, Hugo static blog), giải pháp lưu trữ trên **Amazon S3** luôn là lựa chọn hàng đầu của sinh viên và kỹ sư Cloud vì tính bền vững cực cao (11 số 9), khả năng chịu tải gần như vô hạn và chi phí thì "rẻ như cho".

Tuy nhiên, có một thói quen rất phổ biến (và cũng rất nguy hiểm) mà nhiều bạn mới bắt đầu thường làm theo các bài hướng dẫn cũ: Bật tính năng **"Static Website Hosting"**, sau đó mở toang quyền truy cập công khai (Public Read) bằng chính sách `s3:GetObject` cho toàn thế giới.
Cách làm này tiềm ẩn nhiều rủi ro:
* Bucket S3 bị lộ link công khai, rất dễ bị kẻ xấu quét tự động, tải hàng loạt gây tốn tiền băng thông mạng (Data Transfer Out).
* Không hỗ trợ chứng chỉ HTTPS tùy biến cho tên miền riêng nếu dùng trực tiếp link S3.
* Tốc độ tải trang chậm đối với người dùng ở xa do S3 chỉ nằm tại một Region cố định.

---

### Tiêu chuẩn vàng hiện nay: CloudFront kết hợp Origin Access Control (OAC)
Vào năm 2022, AWS đã giới thiệu **Origin Access Control (OAC)** để thay thế hoàn toàn chuẩn cũ Origin Access Identity (OAI). OAC mang lại những nâng cấp vượt bậc:
* Hỗ trợ toàn bộ các AWS Region mới trên toàn cầu.
* Tương thích hoàn hảo với khóa mã hóa AWS KMS (SSE-KMS).
* Cho phép kiểm soát chặt chẽ cả phương thức ghi nếu cần, bảo vệ S3 an toàn 100%.

```
[ Trình duyệt người dùng ]
            | (Truy cập qua HTTPS / HTTP3 tốc độ cao)
            v
[ Amazon CloudFront CDN ] (Mạng lưới trạm biên toàn cầu)
            | (Gửi request có chữ ký AWS SigV4 qua OAC)
            v
[ Amazon S3 Bucket Private ] (Bật chặn Public Access 100%)
```

---

### Các bước thực hành từng bước

#### 1. Giữ Bucket S3 ở trạng thái hoàn toàn Private
Hãy luôn bật tùy chọn **"Block all public access"** khi tạo bucket. Không cần bật "Static website hosting". Hãy coi S3 đơn thuần là một kho chứa dữ liệu thô an toàn.

#### 2. Khởi tạo CloudFront Distribution
* Trong mục **Origin domain**, chọn tên bucket S3 của bạn (ví dụ: `your-bucket-name.s3.ap-southeast-1.amazonaws.com`).
* Tại mục **Origin access**, tích chọn **Origin access control settings (recommended)** và bấm nút tạo OAC mới.
* Chọn chuyển hướng giao thức **Redirect HTTP to HTTPS** trong phần Default Cache Behavior.
* Điền file trang chủ mặc định: `index.html`.

#### 3. Cập nhật chính sách Bucket Policy trên S3
Sau khi tạo, CloudFront sẽ tạo sẵn một đoạn mã chính sách JSON. Bạn chỉ việc copy và dán vào phần Bucket Policy của S3:

```json
{
  "Version": "2012-10-17",
  "Statement": {
    "Sid": "AllowCloudFrontServicePrincipalReadOnly",
    "Effect": "Allow",
    "Principal": {
      "Service": "cloudfront.amazonaws.com"
    },
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::your-bucket-name/*",
    "Condition": {
      "StringEquals": {
        "AWS:SourceArn": "arn:aws:cloudfront::123456789012:distribution/EDFDVBD6EXAMPLE"
      }
    }
  }
}
```

Hãy chú ý điều kiện `AWS:SourceArn`: Điều kiện này đảm bảo rằng **chỉ duy nhất** CloudFront Distribution do chính bạn tạo ra mới được phép đọc file trong bucket, ngăn chặn hoàn toàn việc ai đó lấy cắp dữ liệu từ tài khoản khác.

---

### Mẹo tối ưu chi phí và tăng tốc tải trang

1. **Thiết lập Cache-Control thông minh khi deploy:**  
   Với các file tĩnh có mã băm tên file (như `app.a1b2c3.js`), hãy cấu hình thời gian cache dài hạn lên tới 1 năm:
   ```bash
   aws s3 cp ./build/static s3://your-bucket-name/static \
     --cache-control "public, max-age=31536000, immutable"
   ```
2. **Xử lý điều hướng trang con trong React/Vue (SPA):**  
   Thêm một Custom Error Response trong CloudFront: Khi gặp mã lỗi 403 hoặc 404, trả về file `/index.html` kèm mã trạng thái HTTP 200. Nhờ đó, cơ chế Client-Side Routing (React Router) sẽ hoạt động trơn tru mà không bị lỗi trang trắng khi người dùng nhấn F5.
3. **Tiết kiệm tiền xóa cache (Invalidation):**  
   Mỗi tháng AWS tặng miễn phí 1.000 đường dẫn invalidation đầu tiên. Thay vì xóa toàn bộ `/*`, bạn chỉ nên xóa đúng file `/index.html` mỗi khi có bản cập nhật mới.

---

### Lời kết
Sự kết hợp giữa Amazon S3, CloudFront và Origin Access Control chính là công thức hoàn hảo để xây dựng một website có tốc độ phản hồi tính bằng mili-giây, bảo mật tuyệt đối trước các đợt tấn công mạng và giúp bạn yên tâm không lo phát sinh hóa đơn tiền đám mây bất ngờ.
