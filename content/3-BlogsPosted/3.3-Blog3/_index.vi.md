---
title: "Blog 3"
date: 2026-11-10
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# API ĐÃ CÓ AWS WAF, VÌ SAO VẪN CẦN THROTTLING?

**Bài viết đã chia sẻ trên cộng đồng AWS Study Group.**

**Link bài đăng:** [Xem bài viết trên Facebook](https://www.facebook.com/share/p/197T9SMqNq/)

## Nội dung bài viết

Khi một API liên tục nhận lượng lớn request, chỉ sử dụng AWS WAF chưa đủ để kiểm soát toàn bộ lưu lượng đi đến backend. AWS WAF và API Gateway Throttling đảm nhận hai vai trò khác nhau: một lớp lọc request bất thường từ sớm, lớp còn lại giới hạn tốc độ xử lý trước khi gọi backend.

Kiến trúc minh họa sử dụng **Client → Amazon CloudFront (AWS WAF) → Amazon API Gateway → AWS Lambda**, kết hợp Amazon CloudWatch để giám sát hoạt động của từng lớp.

### Các điểm chính cần nắm

- **AWS WAF Rate-based Rules:** Theo dõi tần suất request theo IP hoặc tiêu chí tổng hợp được cấu hình, giúp hạn chế lưu lượng bất thường trước khi request đến API Gateway.
- **Scope-down Statement:** Cho phép áp dụng quy tắc giới hạn cho endpoint cụ thể như `/api/search`, thay vì toàn bộ website.
- **API Gateway Throttling:** Kiểm soát lưu lượng thông qua Rate Limit và Burst Limit, giúp giảm áp lực lên AWS Lambda.
- **HTTP 403 và 429:** AWS WAF trả về HTTP 403 mặc định khi chặn request, trong khi API Gateway có thể trả về HTTP 429 khi vượt giới hạn throttling.
- **Bảo vệ đường truy cập trực tiếp:** Nếu endpoint `execute-api` mặc định vẫn truy cập được, client có thể bỏ qua lớp WAF gắn với CloudFront.
- **Giám sát với CloudWatch:** Kết hợp WAF logs, API Gateway metrics/access logs và Lambda metrics để xác định request bị chặn hoặc xử lý tại lớp nào.

### Ứng dụng thực tế

Đối với API công khai, có thể kết hợp AWS WAF và API Gateway Throttling để hạn chế request bất thường, kiểm soát tải backend và giảm nguy cơ ảnh hưởng đến người dùng hợp lệ.

Nên bắt đầu kiểm tra WAF Rate-based Rules bằng hành động **Count**, sau đó đánh giá lưu lượng trước khi chuyển sang **Block**. Đồng thời, cần kiểm tra đường truy cập trực tiếp đến API Gateway và theo dõi logs để xác minh hiệu quả của từng lớp bảo vệ.

## Hình ảnh

<img width="2438" height="540" alt="image" src="https://github.com/user-attachments/assets/af4f9c23-c8cc-4aaa-bad0-cc7474a36884" />

## Tài liệu tham khảo

- [AWS Documentation – Rate-based Rule Settings in AWS WAF](https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-rate-based-high-level-settings.html)
- [AWS Documentation – API Gateway Request Throttling](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html)
