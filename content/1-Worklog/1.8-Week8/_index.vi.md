---
title: "Worklog Tuần 8"
date: 2025-09-29
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

# Tuần 8: Giám sát hệ thống, Cảnh báo và Nhật ký tập trung (Amazon CloudWatch)

### Mục tiêu tuần 8:
* Làm chủ 3 trụ cột giám sát hệ thống (Metrics, Logs, Traces) với Amazon CloudWatch và AWS X-Ray.
* Thiết lập các cảnh báo tự động (CloudWatch Alarms) tích hợp Amazon SNS để gửi thông báo tức thì khi có sự cố.
* Khai thác sức mạnh của CloudWatch Logs Insights để phân tích và truy vết lỗi từ hàng triệu bản ghi nhật ký.

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Phân biệt Metric tiêu chuẩn và Metric tùy biến (Custom Metrics).<br>- Cài đặt và cấu hình phần mềm giám sát CloudWatch Unified Agent lên máy chủ EC2 để thu thập các thông số nâng cao như tỷ lệ dùng RAM và dung lượng ổ đĩa trống. | 29/09/2025 | 29/09/2025 | [Hướng dẫn CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html) |
| **Thứ 3** | - Thiết kế bảng điều khiển CloudWatch Dashboard trực quan: Hiển thị tải CPU, RAM, tỷ lệ lỗi HTTP 5xx của Load Balancer và độ trễ phản hồi.<br>- Tùy chỉnh khoảng thời gian làm mới dữ liệu và sắp xếp biểu đồ khoa học. | 30/09/2025 | 30/09/2025 | [CloudWatch Dashboards](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html) |
| **Thứ 4** | - Cài đặt CloudWatch Alarm kích hoạt khi CPU vượt quá ngưỡng 80% trong 2 chu kỳ đo liên tiếp (5 phút).<br>- Tích hợp cảnh báo với Amazon SNS để gửi email khẩn cấp đến hòm thư cá nhân và gửi tin nhắn cảnh báo vào kênh Slack của nhóm. | 01/10/2025 | 01/10/2025 | [Cảnh báo CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| **Thứ 5** | - Cấu hình thời hạn lưu log (Retention Policy) cho các Log Group để tránh lãng phí tiền lưu trữ log cũ.<br>- Thực hành viết truy vấn trên CloudWatch Logs Insights: Lọc các bản ghi lỗi `ERROR`, đếm số lượng lỗi theo mã phản hồi và tính bách phân vị độ trễ (`p95`, `p99`). | 02/10/2025 | 02/10/2025 | [CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) |
| **Thứ 6** | - Bật tính năng truy vết phân tán AWS X-Ray trên API Gateway và Lambda.<br>- Xem sơ đồ tương tác dịch vụ (Service Map) để phát hiện chính xác hàm nào hoặc câu truy vấn cơ sở dữ liệu nào đang gây nghẽn cổ chai.<br>- Viết báo cáo tuần 8. | 03/10/2025 | 03/10/2025 | [Tài liệu AWS X-Ray](https://docs.aws.amazon.com/xray/) |

### Kết quả đạt được & Bài học rút ra:
* **Tư duy giám sát chủ động:** Chuyển từ việc bị động chờ khách hàng báo lỗi sang việc nhận cảnh báo tự động qua điện thoại ngay khi hệ thống có dấu hiệu bất thường.
* **Tốc độ khoanh vùng sự cố:** Nhờ Logs Insights, việc tìm ra nguyên nhân gốc rễ và dòng code bị crash chỉ mất vài giây thay vì phải SSH vào từng server đọc từng file log thủ công.
* **Nhìn rõ luồng đi của request:** AWS X-Ray giúp bóc tách từng mili-giây thời gian xử lý qua các microservice, là công cụ không thể thiếu khi tối ưu hiệu năng.
