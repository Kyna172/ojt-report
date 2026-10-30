---
title: "Worklog Tuần 11"
date: 2025-10-20
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

# Tuần 11: Xây dựng bài thực hành Workshop & Hoàn thiện tài liệu kỹ thuật

### Mục tiêu tuần 11:
* Thiết kế và xây dựng hoàn chỉnh kịch bản bài thực hành chuyên sâu: "Truy cập Amazon S3 an toàn qua mạng lai sử dụng VPC Endpoints".
* Khởi tạo môi trường mạng lai giả lập qua CloudFormation kết hợp VPN Site-to-Site mã nguồn mở strongSwan.
* Biên soạn tài liệu hướng dẫn từng bước chi tiết theo chuẩn song ngữ Anh - Việt, có hình ảnh minh họa và lệnh kiểm tra thực tế.

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Xác định phạm vi và kiến trúc bài lab: Giúp hệ thống máy chủ On-Premises và VPC truy cập kho lưu trữ S3 hoàn toàn trên mạng riêng, không đi qua Internet.<br>- Chạy Stack CloudFormation tạo 2 VPC: Một VPC đại diện cho Cloud và một VPC giả lập hạ tầng trung tâm dữ liệu On-Premises kết nối qua kênh VPN. | 20/10/2025 | 20/10/2025 | [Tài liệu AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/) |
| **Thứ 3** | - Tạo một Gateway VPC Endpoint cho S3; kiểm tra bảng định tuyến Route Table tự động bổ sung danh sách tiền tố (Prefix List) của S3.<br>- Dùng EC2 trong Private Subnet không có Internet Gateway kiểm tra tải và upload file lên S3 thành công.<br>- Chụp ảnh màn hình, lưu lại câu lệnh CLI và viết nội dung phần 1 của Workshop. | 21/10/2025 | 21/10/2025 | [Gateway VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html) |
| **Thứ 4** | - Khởi tạo Interface VPC Endpoint (AWS PrivateLink) gắn card mạng ảo ENI vào từng Private Subnet.<br>- Kiểm tra địa chỉ IP nội bộ và các tên miền DNS riêng do endpoint sinh ra.<br>- Dùng AWS Systems Manager Session Manager đăng nhập vào máy ảo On-Premises để thử nghiệm kết nối. | 22/10/2025 | 22/10/2025 | [Interface VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html) |
| **Thứ 5** | - Cấu hình Route 53 Private Hosted Zone để xử lý phân giải tên miền (DNS Resolution) từ máy chủ On-Premises trỏ về địa chỉ IP của Interface Endpoint.<br>- Kiểm tra độ phân giải tên miền bằng lệnh `dig` và `nslookup`.<br>- Cấu hình Endpoint Policy nhằm siết chặt quyền hạn, chỉ cho phép đọc từ một bucket duy nhất. | 23/10/2025 | 23/10/2025 | [Tài liệu Route 53 Resolver](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html) |
| **Thứ 6** | - Đóng vai một người thực hành mới, làm lại toàn bộ bài lab từ đầu đến cuối chỉ dựa trên tài liệu đã viết để phát hiện những chỗ hướng dẫn còn thiếu sót hoặc khó hiểu.<br>- Viết quy trình dọn dẹp (Cleanup) chi tiết đảm bảo người học xóa sạch mọi tài nguyên có phát sinh chi phí.<br>- Nộp báo cáo tuần 11. | 24/10/2025 | 24/10/2025 | Quy chuẩn Workshop FCAJ |

### Kết quả đạt được & Bài học rút ra:
* **Hiểu sâu bản chất kỹ thuật VPC Endpoint:** Phân biệt rành mạch khi nào nên dùng Gateway Endpoint (miễn phí, chỉ dùng nội bộ trong VPC) và khi nào bắt buộc phải dùng Interface Endpoint (PrivateLink có tính phí, nhưng định tuyến được từ hạ tầng On-Premise hoặc Transit Gateway).
* **Kỹ năng sư phạm và viết tài liệu:** Hiểu rằng viết một bài lab kỹ thuật tốt đòi hỏi sự tỉ mỉ rất cao, phải giải thích rõ lý do tại sao lại cấu hình như vậy chứ không chỉ đơn thuần là bảo người đọc bấm nút nào.
* **Quy trình đóng gói tài nguyên an toàn:** Luôn luôn đính kèm phần dọn dẹp cẩn thận để bảo vệ tài khoản của người thực hành không bị tính tiền ngoài ý muốn.
