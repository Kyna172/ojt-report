---
title: "Worklog Tuần 3"
date: 2025-08-25
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

# Tuần 3: Dịch vụ tính toán linh hoạt, Cân bằng tải & Tự động co giãn

### Mục tiêu tuần 3:
* Nắm vững các họ máy chủ Amazon EC2, mô hình chi phí (On-Demand, Spot, Savings Plans) và các loại ổ lưu trữ EBS.
* Thiết lập bộ cân bằng tải Application Load Balancer (ALB) với Target Group và cơ chế kiểm tra sức khỏe máy chủ (Health Checks).
* Xây dựng cụm máy chủ tự động co giãn Auto Scaling Group (ASG) đảm bảo khả năng chịu lỗi và tính sẵn sàng cao (High Availability).

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Phân biệt các dòng máy chủ EC2: T (General Purpose), C (Compute), R (Memory Optimized).<br>- Viết đoạn bash script User Data để máy chủ tự động cài đặt Nginx và in trang HTML hiển thị ID instance khi vừa khởi động. | 25/08/2025 | 25/08/2025 | [EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/) |
| **Thứ 3** | - Nghiên cứu các loại ổ đĩa EBS: gp3, io2, st1.<br>- Thực hành tạo ổ đĩa gp3 mới, gắn vào máy ảo Linux, phân vùng, định dạng file system ext4 và mount vào thư mục hệ thống.<br>- Tạo Snapshot sao lưu EBS và thử phục hồi ổ đĩa từ snapshot. | 26/08/2025 | 26/08/2025 | [Tài liệu Amazon EBS](https://docs.aws.amazon.com/ebs/) |
| **Thứ 4** | - Khởi tạo Application Load Balancer (ALB) nằm trên các Public Subnet.<br>- Thiết lập Target Group và cấu hình đường dẫn kiểm tra tình trạng sống còn (`/health`).<br>- Gắn 2 máy chủ ở 2 AZ khác nhau vào Target Group và quan sát ALB phân phối tải xoay vòng (round-robin). | 27/08/2025 | 27/08/2025 | [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/) |
| **Thứ 5** | - Tạo một Amazon Machine Image (AMI) hoàn chỉnh từ máy chủ web mẫu.<br>- Xây dựng Launch Template sử dụng AMI vừa tạo kèm theo Security Group chuẩn.<br>- Cấu hình Auto Scaling Group (ASG) với Min=2, Desired=2, Max=4 phân bổ đều trên 2 AZ. | 28/08/2025 | 28/08/2025 | [EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/) |
| **Thứ 6** | - Cài đặt công cụ `stress` trên máy ảo để đẩy tải CPU lên cao kiểm thử tính năng tự động giãn rộng (Scale Out).<br>- Quan sát CloudWatch phát hiện quá tải và kích hoạt tạo thêm máy chủ mới trong ASG.<br>- Dọn dẹp tài nguyên ALB và ASG; tổng hợp kiến thức đã học vào báo cáo tuần 3. | 29/08/2025 | 29/08/2025 | [AWS Auto Scaling](https://docs.aws.amazon.com/autoscaling/) |

### Kết quả đạt được & Bài học rút ra:
* **Hiểu bản chất tính sẵn sàng cao:** Tự tay xây dựng được mô hình hệ thống có khả năng tự phục hồi (self-healing), nếu một máy chủ hoặc cả một AZ bị sự cố thì hệ thống vẫn duy trì hoạt động bình thường.
* **Tự động hóa với Launch Template & User Data:** Không còn phải cài đặt thủ công từng phần mềm trên server, tất cả đều được đóng gói thành mẫu cấu hình sẵn sàng nhân bản.
* **Tư duy tối ưu chi phí hạ tầng:** Hiểu cách dùng Auto Scaling để chỉ trả tiền cho tài nguyên máy chủ khi có lượng truy cập thật sự, hạ thấp số lượng instance khi vào ban đêm vắng khách.
