---
title: "Worklog Tuần 5"
date: 2025-09-08
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

# Tuần 5: Quản trị cơ sở dữ liệu quan hệ và NoSQL (Amazon RDS & DynamoDB)

### Mục tiêu tuần 5:
* Hiểu rõ ưu thế của dịch vụ cơ sở dữ liệu có quản lý (Managed Databases) so với việc tự dựng DB trên EC2.
* Triển khai cụm Amazon RDS PostgreSQL với tính năng sao chép dự phòng đa vùng Multi-AZ và Read Replica.
* Nắm chắc tư duy thiết kế dữ liệu NoSQL trên Amazon DynamoDB: Partition Key, Sort Key và Global Secondary Index (GSI).

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Tạo DB Subnet Group chứa các Private Subnet trên nhiều AZ trong `Lab-VPC`.<br>- Khởi tạo cơ sở dữ liệu RDS PostgreSQL kiểu Multi-AZ, cấu hình Security Group chỉ cho phép kết nối từ dải IP của tầng ứng dụng. | 08/09/2025 | 08/09/2025 | [Hướng dẫn Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) |
| **Thứ 3** | - Kết nối bảo mật vào RDS từ máy chủ nội bộ qua công cụ psql.<br>- Bật cơ chế sao lưu tự động (Automated Backups) và chụp snapshot thủ công.<br>- Thử nghiệm tính năng ép chuyển đổi dự phòng (Reboot with Failover) để quan sát thời gian phục hồi và thay đổi DNS của RDS. | 09/09/2025 | 09/09/2025 | [Cơ chế Multi-AZ RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html) |
| **Thứ 4** | - Tạo một bản sao chỉ đọc (Read Replica) để chia tải đọc cho hệ thống báo cáo/truy vấn nặng.<br>- Cấu hình DB Parameter Group và quan sát chỉ số hiệu năng trên RDS Performance Insights. | 10/09/2025 | 10/09/2025 | [RDS Read Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html) |
| **Thứ 5** | - Tìm hiểu sự khác biệt cơ bản giữa SQL và NoSQL, kiến trúc phân tán phi máy chủ của DynamoDB.<br>- Tạo bảng DynamoDB với Khóa phân vùng (Partition Key - `userId`) và Khóa sắp xếp (Sort Key - `timestamp`).<br>- So sánh chế độ On-Demand và Provisioned (RCU/WCU). | 11/09/2025 | 11/09/2025 | [Tài liệu DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) |
| **Thứ 6** | - Tạo chỉ mục phụ toàn cục (Global Secondary Index - GSI) để truy vấn theo các thuộc tính khác linh hoạt.<br>- Viết script Python (thư viện boto3) để chèn và truy vấn dữ liệu vào DynamoDB.<br>- Xóa RDS để tiết kiệm chi phí học tập và nộp báo cáo tuần 5. | 12/09/2025 | 12/09/2025 | [Chỉ mục GSI DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GSI.html) |

### Kết quả đạt được & Bài học rút ra:
* **Khả năng chịu lỗi của dữ liệu:** Chứng kiến cơ chế đồng bộ dữ liệu tự động giữa 2 AZ của RDS, máy chủ chính hỏng thì máy chủ dự phòng lập tức tiếp quản gần như tức thời.
* **Tối ưu hóa hiệu năng đọc:** Nhận thấy Read Replica là chìa khóa vàng giúp giải phóng gánh nặng truy vấn thống kê khỏi cơ sở dữ liệu nghiệp vụ chính.
* **Thay đổi tư duy thiết kế schema:** Với DynamoDB, việc thiết kế bảng phải dựa hoàn toàn trên các mẫu truy vấn (Access Patterns) mong muốn ngay từ đầu, thay vì chuẩn hóa dữ liệu như bảng quan hệ truyền thống.
