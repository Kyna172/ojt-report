---
title: "Worklog Tuần 2"
date: 2025-08-18
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

# Tuần 2: Nền tảng mạng chuyên sâu trên AWS (Amazon VPC)

### Mục tiêu tuần 2:
* Nắm chắc kiến trúc mạng riêng ảo Amazon Virtual Private Cloud (Amazon VPC).
* Tự tay thiết kế và cấu hình một VPC hoàn chỉnh đa vùng sẵn sàng (Multi-AZ) gồm Public Subnet và Private Subnet.
* Hiểu rõ cơ chế định tuyến qua Internet Gateway, NAT Gateway và sự khác biệt giữa Security Group và Network ACL.

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Học cách tính toán dải địa chỉ IPv4 theo chuẩn CIDR (`10.0.0.0/16`).<br>- Khởi tạo VPC tùy chỉnh mang tên `Lab-VPC` trải dài trên 2 Availability Zones (`ap-southeast-1a` và `ap-southeast-1b`). | 18/08/2025 | 18/08/2025 | [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/) |
| **Thứ 3** | - Tạo 2 Public Subnet và 2 Private Subnet trong `Lab-VPC`.<br>- Tạo và gắn Internet Gateway (IGW) vào VPC.<br>- Cấu hình Route Table cho Public Subnet với đích đến `0.0.0.0/0` trỏ về IGW. | 19/08/2025 | 19/08/2025 | [VPC Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html) |
| **Thứ 4** | - Cấp phát một địa chỉ Elastic IP (EIP) và tạo NAT Gateway đặt tại Public Subnet.<br>- Cập nhật Private Route Table để cho phép máy chủ trong Private Subnet truy cập internet tải gói cập nhật qua NAT Gateway.<br>- Kiểm tra lệnh `yum update` từ máy chủ private thành công. | 20/08/2025 | 20/08/2025 | [VPC NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) |
| **Thứ 5** | - So sánh chi tiết Security Group (Stateful - lọc ở cấp độ Instance) và NACL (Stateless - lọc ở cấp độ Subnet).<br>- Thử nghiệm chặn một địa chỉ IP cụ thể bằng quy tắc Inbound Deny trên NACL.<br>- Tìm hiểu cơ chế ghi log lưu lượng mạng VPC Flow Logs. | 21/08/2025 | 21/08/2025 | [Bảo mật VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html) |
| **Thứ 6** | - Tìm hiểu sơ lược về VPC Peering và giải pháp AWS Transit Gateway khi kết nối nhiều VPC.<br>- Xóa bỏ NAT Gateway và giải phóng Elastic IP ngay sau buổi thực hành để tránh phát sinh chi phí duy trì.<br>- Vẽ sơ đồ luồng dữ liệu mạng và nộp báo cáo tuần 2. | 22/08/2025 | 22/08/2025 | [VPC Peering Guide](https://docs.aws.amazon.com/vpc/latest/peering/) |

### Kết quả đạt được & Bài học rút ra:
* **Tư duy thiết kế mạng an toàn:** Hiểu tường tận nguyên tắc phòng thủ theo chiều sâu: Máy chủ web hướng người dùng đặt ở Public Subnet, cơ sở dữ liệu và logic nghiệp vụ cốt lõi bắt buộc nằm ở Private Subnet.
* **Ý thức tối ưu chi phí:** Trải nghiệm thực tế việc NAT Gateway tính tiền theo giờ và dung lượng dữ liệu đi qua, rèn luyện thói quen tắt/xóa tài nguyên có tính phí ngay khi kết thúc bài lab.
* **Kỹ năng gỡ rối (troubleshooting) mạng:** Biết cách kiểm tra Route Table và Security Group khi một máy chủ không thể kết nối ra internet hoặc không nhận được gói tin phản hồi.
