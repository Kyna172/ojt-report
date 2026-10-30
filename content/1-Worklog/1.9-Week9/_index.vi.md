---
title: "Worklog Tuần 9"
date: 2025-10-06
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

# Tuần 9: Đóng gói và Vận hành ứng dụng dạng Container (Docker, ECR & ECS)

### Mục tiêu tuần 9:
* Thành thạo kỹ thuật đóng gói ứng dụng bằng Docker với kỹ thuật Multi-stage build tối ưu kích thước image.
* Quản lý kho chứa container bảo mật và quét lỗ hổng bảo mật tự động trên Amazon Elastic Container Registry (ECR).
* Triển khai cụm dịch vụ container phi máy chủ với Amazon Elastic Container Service (ECS) chạy trên hạ tầng AWS Fargate.

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Học kiến thức nền tảng về Container, cơ chế layer của Docker và các nguyên tắc bảo mật khi viết Dockerfile.<br>- Áp dụng kỹ thuật Multi-stage build cho ứng dụng web, giảm dung lượng image từ 850MB xuống chỉ còn 65MB. | 06/10/2025 | 06/10/2025 | [Tài liệu Docker](https://docs.docker.com/) |
| **Thứ 3** | - Tạo kho lưu trữ private repository trên Amazon ECR, bật tính năng khóa thẻ phiên bản (Immutable Tags).<br>- Kích hoạt tính năng tự động quét lỗ hổng bảo mật (Scan on push) để kiểm tra các mã lỗi CVE.<br>- Đăng nhập Docker qua CLI bằng lệnh `aws ecr get-login-password` và đẩy image lên kho ECR. | 07/10/2025 | 07/10/2025 | [Hướng dẫn Amazon ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/) |
| **Thứ 4** | - Nghiên cứu 3 khái niệm cốt lõi của ECS: Cụm (Cluster), Định nghĩa tác vụ (Task Definition) và Dịch vụ (Service).<br>- Viết file Task Definition quy định mức CPU, RAM, cổng kết nối và các biến môi trường cấu hình ứng dụng. | 08/10/2025 | 08/10/2025 | [Tài liệu Amazon ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/) |
| **Thứ 5** | - Triển khai một ECS Service trên nền tảng phi máy chủ AWS Fargate, chạy bên trong Private Subnet và đứng sau ALB.<br>- Không cần quản lý bất kỳ máy chủ EC2 máy chủ chủ nào, chỉ định mức CPU/RAM là Fargate tự động chạy.<br>- Kiểm tra quy trình cập nhật phiên bản mới cuốn chiếu (Rolling Update) không gây gián đoạn dịch vụ (Zero downtime). | 09/10/2025 | 09/10/2025 | [Hướng dẫn AWS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html) |
| **Thứ 6** | - Cấu hình tính năng tự động tăng giảm số lượng task (Service Auto Scaling) dựa trên số lượng request đổ về Load Balancer.<br>- Đọc báo cáo quét bảo mật của ECR và sửa các thư viện có nguy cơ rủi ro.<br>- Dọn dẹp tài nguyên và nộp báo cáo tuần 9. | 10/10/2025 | 10/10/2025 | [Tự động co giãn ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-auto-scaling.html) |

### Kết quả đạt được & Bài học rút ra:
* **Hiệu quả của Multi-stage build:** Loại bỏ toàn bộ các công cụ biên dịch thừa khỏi image cuối, vừa giảm mạnh thời gian tải vừa thu hẹp bề mặt tấn công của kẻ xấu.
* **Sự tiện lợi của AWS Fargate:** Không còn phải đau đầu tính toán nâng cấp hệ điều hành máy chủ hay lo lắng dung lượng đĩa của cluster, mọi thứ đều được trừu tượng hóa thành từng tác vụ độc lập.
* **Quy trình triển khai không gián đoạn:** Hiểu sâu sắc cách ECS và Load Balancer phối hợp kiểm tra sức khỏe của container mới trước khi ngắt kết nối container cũ, đem lại trải nghiệm mượt mà cho người dùng.
