---
title: "Worklog Tuần 7"
date: 2025-09-22
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

# Tuần 7: Bảo mật, Quản lý danh tính & Tuân thủ quy chuẩn (Security & Governance)

### Mục tiêu tuần 7:
* Nắm vững nguyên tắc trao quyền tối thiểu (Principle of Least Privilege) trong AWS Identity and Access Management (IAM).
* Triển khai mã hóa dữ liệu tĩnh và dữ liệu truyền tải với dịch vụ quản lý khóa AWS Key Management Service (KMS).
* Quản lý thông tin mật với AWS Secrets Manager và thiết lập cơ chế giám sát tuân thủ, kiểm toán vết gọi API với AWS CloudTrail.

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Nghiên cứu cơ chế xét duyệt chính sách phân quyền IAM: Phủ quyết rõ ràng (Explicit Deny) luôn có quyền lực cao nhất.<br>- Viết các IAM Policy tùy chỉnh có gắn điều kiện (Condition Keys: `aws:SourceIP`, `aws:PrincipalArn`).<br>- Thực hành giả lập danh tính (Assume Role) và sử dụng chứng chỉ tạm thời cấp bởi AWS STS. | 22/09/2025 | 22/09/2025 | [Cơ chế xét quyền IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html) |
| **Thứ 3** | - Tạo khóa mã hóa đối xứng Customer Managed Key (CMK) trong AWS KMS.<br>- Bật tính năng tự động xoay vòng khóa hàng năm (Key Rotation).<br>- Thử nghiệm mã hóa và giải mã chuỗi ký tự qua CLI; áp dụng khóa KMS để mã hóa ổ cứng EBS và S3 Bucket. | 23/09/2025 | 23/09/2025 | [Hướng dẫn AWS KMS](https://docs.aws.amazon.com/kms/) |
| **Thứ 4** | - Lưu trữ mật khẩu kết nối cơ sở dữ liệu và API Key bảo mật vào AWS Secrets Manager.<br>- Tìm hiểu cơ chế tự động đổi mật khẩu định kỳ của Secrets Manager kết hợp với hàm Lambda.<br>- Viết mã nguồn Python lấy mật khẩu động lúc chạy ứng dụng, tuyệt đối không hardcode mật khẩu vào git. | 24/09/2025 | 24/09/2025 | [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/) |
| **Thứ 5** | - Kích hoạt AWS CloudTrail ghi nhận toàn bộ hoạt động gọi API trên mọi Region.<br>- Dùng Amazon Athena viết câu lệnh SQL truy vấn trực tiếp file log JSON của CloudTrail để điều tra sự cố.<br>- Thiết lập chuông báo Amazon SNS gửi email cảnh báo khi có sự cố đăng nhập sai quyền `AccessDenied`. | 25/09/2025 | 25/09/2025 | [Tài liệu CloudTrail](https://docs.aws.amazon.com/awscloudtrail/) |
| **Thứ 6** | - Cấu hình tường lửa ứng dụng web AWS WAF gắn trước Application Load Balancer.<br>- Bật các bộ quy tắc phòng thủ có sẵn (AWS Managed Rules) chống tấn công SQL Injection và XSS.<br>- Tổng kết bài học bảo mật và nộp báo cáo tuần 7. | 26/09/2025 | 26/09/2025 | [Bảo mật AWS WAF](https://docs.aws.amazon.com/waf/) |

### Kết quả đạt được & Bài học rút ra:
* **Tuyệt đối không lưu mật khẩu trong code:** Hình thành thói quen loại bỏ hoàn toàn mật mã tĩnh, token khỏi source code và cấu hình hệ thống.
* **Khả năng truy vết kiểm toán:** Nắm được cách truy xuất lịch sử ai đã làm gì, từ IP nào, vào thời điểm nào trên hệ sinh thái AWS chỉ trong vài phút.
* **Bảo vệ nhiều lớp (Defense in Depth):** Kết hợp chặt chẽ giữa tường lửa lớp mạng, kiểm soát danh tính danh mục và mã hóa dữ liệu đầu cuối.
