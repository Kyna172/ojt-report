---
title: "Worklog Tuần 10"
date: 2025-10-13
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

# Tuần 10: Tự động hóa hạ tầng (IaC) và Quy trình CI/CD

### Mục tiêu tuần 10:
* Tiếp cận tư duy quản lý hạ tầng bằng mã nguồn (Infrastructure as Code - IaC) với AWS CloudFormation và Terraform.
* Xây dựng luồng tích hợp và triển khai liên tục (CI/CD Pipeline) hoàn toàn tự động bằng GitHub Actions.
* Ứng dụng xác thực không mật khẩu (OIDC) giữa GitHub và AWS, tự động hóa kiểm thử mã nguồn và triển khai ứng dụng.

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Nghiên cứu khái niệm IaC: Quản lý trạng thái (State), phát hiện lệch cấu hình (Drift Detection) và tính lũy quyền (Idempotency).<br>- Viết mẫu CloudFormation bằng cú pháp YAML định nghĩa một S3 Bucket chuẩn bảo mật (bật versioning, mã hóa mặc định, gắn chính sách chặn public). | 13/10/2025 | 13/10/2025 | [Tài liệu CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/) |
| **Thứ 3** | - Thực hành triển khai Stack CloudFormation qua dòng lệnh AWS CLI.<br>- Tìm hiểu cấu trúc cơ bản của Terraform: Provider, Resource, Variable, Output và lưu trữ file trạng thái từ xa (Remote State) trên S3 kết hợp DynamoDB State Locking. | 14/10/2025 | 14/10/2025 | [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) |
| **Thứ 4** | - Tạo workflow GitHub Actions tự động kích hoạt khi có lệnh đẩy mã (`push`) lên nhánh `main`.<br>- Cấu hình xác thực định danh OIDC (OpenID Connect) giữa GitHub và AWS IAM, loại bỏ hoàn toàn việc lưu Access Key tĩnh trong kho bí mật GitHub Secrets. | 15/10/2025 | 15/10/2025 | [Cấu hình GitHub OIDC với AWS](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services) |
| **Thứ 5** | - Viết quy trình CI/CD nhiều bước: Kéo code về -> Cài đặt thư viện -> Chạy Unit Test -> Quét chất lượng code Linter -> Đóng gói build dự án Hugo/Next.js.<br>- Tự động tải tệp tin build lên S3 và kích hoạt xóa bộ nhớ đệm CloudFront Invalidation. | 16/10/2025 | 16/10/2025 | [Tài liệu GitHub Actions](https://docs.github.com/en/actions) |
| **Thứ 6** | - Thiết lập Branch Protection Rules trên GitHub, bắt buộc toàn bộ bài kiểm tra tự động phải màu xanh mới cho phép merge code vào nhánh chính.<br>- Thử nghiệm cố tình tạo lỗi kiểm thử trên một nhánh phụ để kiểm chứng cơ chế ngăn chặn mã lỗi lọt vào production.<br>- Nộp báo cáo tuần 10. | 17/10/2025 | 17/10/2025 | [Thực tiễn AWS DevOps](https://aws.amazon.com/devops/) |

### Kết quả đạt được & Bài học rút ra:
* **Từ bỏ thói quen ClickOps:** Chuyển dịch hoàn toàn từ thao tác click chuột thủ công sang quản lý toàn bộ hệ thống bằng code được lưu vết lịch sử phiên bản trên Git.
* **Bảo mật tối tân với OIDC:** Không còn nỗi lo rò rỉ Access Key trên mạng vì toàn bộ quyền truy cập được cấp phát bằng token tạm thời có thời hạn ngắn.
* **Tốc độ bàn giao sản phẩm vượt bậc:** Rút ngắn thời gian triển khai từ 25 phút thủ công đầy rủi ro nhầm lẫn xuống còn chưa đầy 2 phút tự động, ổn định và chính xác 100%.
