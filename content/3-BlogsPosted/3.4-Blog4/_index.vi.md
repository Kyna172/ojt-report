---
title: "Blog 4"
date: 2026-11-10
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# AMAZON BEDROCK: KIỂM SOÁT REQUEST VÀ TOKEN USAGE TRƯỚC KHI CHI PHÍ TĂNG CAO

**Bài viết đã chia sẻ trên cộng đồng AWS Study Group.**

**Link bài đăng:** [Xem bài viết trên Facebook](https://www.facebook.com/share/p/1cJCsM4u1G/)

## Nội dung bài viết

Khi triển khai ứng dụng Generative AI với Amazon Bedrock, việc kiểm soát số lượng request chưa đủ để quản lý chi phí hiệu quả. Một request hợp lệ vẫn có thể tiêu thụ nhiều token nếu prompt dài hoặc output lớn, đặc biệt khi ứng dụng phục vụ nhiều khách hàng (tenant).

Để hạn chế chi phí ngoài dự kiến, có thể xây dựng kiến trúc kết hợp **Amazon CloudFront, AWS WAF, API Gateway, AWS Lambda, DynamoDB và Amazon Bedrock**, cùng các dịch vụ giám sát và phân tích mức sử dụng.

### Các điểm chính cần nắm

- **AWS WAF và Amazon CloudFront:** Lọc lưu lượng bất thường từ lớp edge bằng Rate-based Rules, giúp hạn chế request không cần thiết trước khi đi vào hệ thống.
- **Amazon API Gateway:** Thực hiện xác thực, phân quyền và throttling thông qua Rate Limit và Burst Limit, giúp kiểm soát tốc độ request trước backend.
- **AWS Lambda và Amazon DynamoDB:** Xây dựng Quota Controller để kiểm tra hạn mức request hoặc token theo từng tenant trước khi gọi Bedrock.
- **Atomic và Conditional Updates:** Hỗ trợ cập nhật quota an toàn khi nhiều request được xử lý đồng thời, tránh sai lệch dữ liệu sử dụng.
- **Token Usage Tracking:** Ước tính token trước inference và đối chiếu với mức sử dụng thực tế sau khi Bedrock trả kết quả.
- **Amazon CloudWatch và SNS:** Theo dõi invocation, input/output token và gửi cảnh báo khi mức sử dụng vượt ngưỡng theo dõi.
- **Amazon S3 và Athena:** Lưu trữ và phân tích dữ liệu usage theo tenant, mô hình hoặc thời gian để hỗ trợ quản lý chi phí chi tiết hơn.

### Ứng dụng thực tế

Kiến trúc này phù hợp với các ứng dụng AI phục vụ nhiều người dùng hoặc tenant, nơi cần giới hạn mức sử dụng riêng cho từng đối tượng và giảm nguy cơ phát sinh chi phí do request lặp lại hoặc sử dụng token quá mức.

Với hệ thống nhỏ, có thể bắt đầu bằng **Lambda, DynamoDB và CloudWatch**, sau đó bổ sung S3 và Athena khi cần phân tích usage chuyên sâu.

Cần lưu ý rằng quota ứng dụng phải xử lý các trường hợp request đồng thời, retry và chênh lệch giữa token ước tính với thực tế. Đây là cơ chế kiểm soát mức sử dụng, không phải giới hạn chi phí tuyệt đối.

## Hình ảnh

<img width="3754" height="540" alt="image" src="https://github.com/user-attachments/assets/7e10d331-3f14-4792-84ad-364ab8d1addb" />

## Tài liệu tham khảo

- [AWS Documentation – Amazon Bedrock Quotas](https://docs.aws.amazon.com/bedrock/latest/userguide/quotas.html)
- [AWS Documentation – Model Invocation Logging](https://docs.aws.amazon.com/bedrock/latest/userguide/model-invocation-logging.html)
