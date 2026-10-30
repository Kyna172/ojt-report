---
title: "Worklog Tuần 4"
date: 2025-09-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

# Tuần 4: Dịch vụ lưu trữ đối tượng và Mạng phân phối nội dung (S3 & CloudFront)

### Mục tiêu tuần 4:
* Nắm chắc các lớp lưu trữ của Amazon S3, quản lý vòng đời dữ liệu (Lifecycle) và phân quyền với Bucket Policy.
* Triển khai lưu trữ website tĩnh (Static Website) an toàn trên S3.
* Tối ưu tốc độ tải trang toàn cầu và bảo mật HTTPS với mạng phân phối nội dung Amazon CloudFront sử dụng Origin Access Control (OAC).

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Tìm hiểu các phân lớp lưu trữ trên S3: Standard, Intelligent-Tiering, Standard-IA, One Zone-IA và các tầng Glacier.<br>- Bật tính năng Versioning để chống ghi đè/xóa nhầm dữ liệu và mã hóa mặc định SSE-S3. | 01/09/2025 | 01/09/2025 | [Lớp lưu trữ Amazon S3](https://aws.amazon.com/s3/storage-classes/) |
| **Thứ 3** | - Cấu hình quy tắc vòng đời (S3 Lifecycle Rules): Tự động chuyển các file sau 30 ngày sang Glacier và xóa hẳn các file rác sau 90 ngày.<br>- Tìm hiểu cơ chế sao lưu chéo vùng Cross-Region Replication (CRR). | 02/09/2025 | 02/09/2025 | [Quản lý vòng đời S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html) |
| **Thứ 4** | - Thử nghiệm tải một ứng dụng web tĩnh lên S3.<br>- Phân tích rủi ro bảo mật nếu mở quyền truy cập công khai (Public Read) trực tiếp từ S3 Bucket. | 03/09/2025 | 03/09/2025 | [Hosting Website trên S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) |
| **Thứ 5** | - Tạo CloudFront Distribution trỏ Origin về S3 Bucket ở trạng thái Private hoàn toàn.<br>- Cấu hình Origin Access Control (OAC) để chỉ cho phép duy nhất CloudFront đọc dữ liệu từ S3.<br>- Kích hoạt bắt buộc HTTPS (Redirect HTTP to HTTPS), bật nén dữ liệu Gzip/Brotli. | 04/09/2025 | 04/09/2025 | [Tài liệu CloudFront OAC](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html) |
| **Thứ 6** | - Thực hành tạo Invalidation (`/*`) trên CloudFront khi cập nhật mã nguồn giao diện mới.<br>- Đo lường thời gian phản hồi (Latency) bằng DevTools trước và sau khi có CDN.<br>- Tổng kết nội dung và nộp báo cáo tuần 4. | 05/09/2025 | 05/09/2025 | [Cơ chế Cache CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Expiration.html) |

### Kết quả đạt được & Bài học rút ra:
* **Tư duy bảo mật chuẩn AWS:** Không bao giờ mở public trực tiếp S3 bucket, thay vào đó luôn đóng kín S3 và phân phối nội dung thông qua CloudFront OAC.
* **Chiến lược tối ưu hóa dung lượng:** Nắm vững cách thiết lập Lifecycle giúp doanh nghiệp tự động tiết kiệm hàng nghìn USD chi phí lưu trữ dữ liệu log và tệp tin cũ.
* **Tăng tốc trải nghiệm người dùng:** Nhận thấy sự vượt trội về tốc độ tải trang nhờ các trạm Edge Location nằm gần người dùng cuối.
