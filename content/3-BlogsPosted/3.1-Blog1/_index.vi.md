---
title: "5 bước quản lý chi phí Amazon Bedrock: Không chỉ đơn giản là giảm số lượng token"
date: 2026-11-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# 5 bước quản lý chi phí Amazon Bedrock: Không chỉ đơn giản là giảm số lượng token

**Bài viết đã chia sẻ trên cộng đồng AWS Study Group.**

**Link bài đăng:** [Xem bài viết trên Facebook](https://www.facebook.com/share/p/19UsES7evm/)

## Nội dung bài viết

Khi triển khai các ứng dụng Generative AI trên AWS, chi phí thường được quan tâm thông qua số lượng token sử dụng và mức giá của từng mô hình. Tuy nhiên, khi số lượng người dùng và yêu cầu xử lý tăng lên, một câu hỏi quan trọng được đặt ra: Làm thế nào để biết chi phí phát sinh từ đâu, ai đang sử dụng tài nguyên và làm sao để kiểm soát ngân sách hiệu quả?

Để giải quyết vấn đề này, AWS giới thiệu quy trình quản lý chi phí Amazon Bedrock gồm 5 bước:

### 1. Xác định chi phí

Xác định chi phí phát sinh từ người dùng, nhóm hoặc ứng dụng nào. Có thể sử dụng AWS Cost and Usage Report (CUR 2.0), IAM tags và AWS Cost Explorer để phân loại và theo dõi chi phí theo từng đối tượng.

### 2. Theo dõi mức sử dụng

Sử dụng Model Invocation Logging để ghi nhận các lần gọi mô hình. Dữ liệu được lưu trên Amazon CloudWatch Logs hoặc Amazon S3, giúp phân tích lượng token tiêu thụ và xác định những ứng dụng sử dụng nhiều tài nguyên.

### 3. Kiểm soát ngân sách

AWS đề xuất 3 cấp độ kiểm soát: sử dụng AWS Budgets để cảnh báo khi vượt ngưỡng, kết hợp IAM với tự động hóa để hạn chế truy cập hoặc sử dụng Gateway để chặn yêu cầu ngay khi vượt giới hạn chi phí.

### 4. Tối ưu chi phí

Sử dụng Intelligent Prompt Routing để lựa chọn mô hình phù hợp với từng tác vụ và Prompt Caching để tái sử dụng ngữ cảnh, giảm chi phí xử lý những nội dung lặp lại. Ngoài ra, việc giới hạn token cũng giúp tránh tiêu thụ tài nguyên không cần thiết.

### 5. Đánh giá và cải thiện

Thường xuyên theo dõi các chỉ số như tỷ lệ sử dụng mô hình, yêu cầu thất bại và hiệu quả Prompt Caching. Từ đó điều chỉnh cách sử dụng tài nguyên và chính sách quản lý chi phí phù hợp.

### Kết luận

Năm bước trên tạo thành quy trình liên tục, một vòng lặp có thể lặp lại, giúp việc quản lý chi phí Amazon Bedrock không chỉ dừng ở theo dõi hóa đơn mà còn chủ động kiểm soát và tối ưu trong quá trình vận hành.

## Tài liệu tham khảo

AWS Machine Learning Blog – *Managing Amazon Bedrock costs end to end: A playbook for FinOps and platform teams* (30/10/2026).

[Đọc bài viết gốc trên AWS](https://aws.amazon.com/vi/blogs/machine-learning/managing-amazon-bedrock-costs-end-to-end-a-playbook-for-finops-and-platform-teams/)
