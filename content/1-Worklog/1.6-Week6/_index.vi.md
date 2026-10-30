---
title: "Worklog Tuần 6"
date: 2025-09-15
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

# Tuần 6: Kiến trúc phi máy chủ Serverless (AWS Lambda & API Gateway)

### Mục tiêu tuần 6:
* Làm quen với tư duy lập trình hướng sự kiện (Event-driven) trên nền tảng Serverless AWS Lambda.
* Thiết kế và xuất bản giao diện lập trình ứng dụng RESTful API với Amazon API Gateway.
* Xây dựng trọn vẹn một ứng dụng Serverless CRUD kết nối trực tiếp giữa API Gateway, Lambda và DynamoDB.

### Các công việc triển khai trong tuần:
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ 2** | - Tìm hiểu vòng đời thực thi của AWS Lambda: Khởi động nguội (Cold Start), phân bổ RAM và giới hạn thời gian (Timeout).<br>- Viết hàm Lambda bằng Python xử lý dữ liệu JSON gửi đến.<br>- Gán IAM Execution Role cấp quyền tối thiểu ghi log vào CloudWatch Logs. | 15/09/2025 | 15/09/2025 | [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/) |
| **Thứ 3** | - Tạo REST API trên Amazon API Gateway, định nghĩa tài nguyên (`/items`) và các phương thức HTTP (`GET`, `POST`, `DELETE`).<br>- Cấu hình Lambda Proxy Integration để truyền toàn bộ header, query param và body sang Lambda.<br>- Bật cấu hình CORS để các ứng dụng web frontend khác domain có thể gọi API. | 16/09/2025 | 16/09/2025 | [Tài liệu API Gateway](https://docs.aws.amazon.com/apigateway/) |
| **Thứ 4** | - Lập trình luồng hoàn chỉnh: Client gọi API Gateway -> kích hoạt Lambda -> thực hiện đọc/ghi dữ liệu trên bảng DynamoDB.<br>- Xử lý kiểm tra tính hợp lệ của dữ liệu đầu vào và trả về mã trạng thái HTTP chuẩn (200, 400, 404, 500). | 17/09/2025 | 17/09/2025 | [Xây dựng Serverless App](https://aws.amazon.com/serverless/) |
| **Thứ 5** | - Tìm hiểu cơ chế kích hoạt bất đồng bộ (Asynchronous Invocation): S3 Event Notifications và DynamoDB Streams.<br>- Viết kịch bản: Khi người dùng upload một bức ảnh lên S3, S3 tự động bắn sự kiện gọi Lambda để tạo ảnh thu nhỏ (thumbnail).<br>- Cấu hình Dead-Letter Queue (DLQ) qua Amazon SQS để hứng các sự kiện xử lý lỗi. | 18/09/2025 | 18/09/2025 | [Lambda Event Mapping](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html) |
| **Thứ 6** | - Khám phá dịch vụ điều phối luồng công việc AWS Step Functions.<br>- Dùng Postman kiểm thử tự động toàn bộ bộ API vừa tạo; quan sát log chi tiết trên CloudWatch.<br>- Nộp báo cáo tuần 6. | 19/09/2025 | 19/09/2025 | [AWS Step Functions](https://docs.aws.amazon.com/step-functions/) |

### Kết quả đạt được & Bài học rút ra:
* **Giải phóng khỏi gánh nặng máy chủ:** Trải nghiệm cảm giác tuyệt vời khi phát triển phần mềm mà không phải lo cấu hình OS, vá lỗi bảo mật hạt nhân hay cấu hình cụm máy chủ chịu tải.
* **Tư duy Microservice phi trạng thái:** Code được chia nhỏ thành các hàm đơn nhiệm, chạy độc lập, dễ dàng nâng cấp hoặc sửa lỗi mà không làm gián đoạn toàn bộ ứng dụng.
* **Xử lý sự cố Cold Start:** Hiểu rõ nguyên nhân gây trễ ở lần gọi đầu tiên và cách đóng gói mã nguồn tinh gọn nhất để giữ thời gian phản hồi ở mức mili-giây.
