---
title: "Các bài blogs đã đăng"
date: 2026-11-10
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# Các bài viết kỹ thuật đã chia sẻ tới cộng đồng

Trong quá trình tham gia chương trình **First Cloud AI Journey (FCAJ)**, em đã tìm hiểu và chia sẻ các bài viết kỹ thuật trên cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Nội dung tập trung vào những vấn đề thực tế khi sử dụng AWS, bao gồm quản lý chi phí Amazon Bedrock, kiểm soát ngân sách, bảo vệ API và quản lý mức sử dụng tài nguyên trong các ứng dụng Generative AI.

Dưới đây là 4 bài viết kỹ thuật đã được chia sẻ:

---

### [Blog 1: 5 bước quản lý chi phí Amazon Bedrock: Không chỉ đơn giản là giảm số lượng token](3.1-Blog1/)

- **Chủ đề:** Amazon Bedrock, Generative AI & Tối ưu chi phí
- **Tóm tắt nội dung:** Giới thiệu quy trình 5 bước quản lý chi phí Amazon Bedrock, từ xác định nguồn phát sinh chi phí, theo dõi token usage và kiểm soát ngân sách đến tối ưu tài nguyên bằng Intelligent Prompt Routing, Prompt Caching và đánh giá hiệu quả vận hành.

---

### [Blog 2: Đặt AWS Budget 10 USD, vì sao hóa đơn vẫn có thể vượt 10 USD?](3.2-Blog2/)

- **Chủ đề:** AWS Budgets, Quản lý ngân sách & Cloud Cost Management
- **Tóm tắt nội dung:** Làm rõ sự khác biệt giữa cảnh báo ngân sách và giới hạn chi tiêu thực tế trên AWS. Giới thiệu cách kết hợp AWS Budgets, Budgets Actions, Cost Anomaly Detection và Cost Explorer để theo dõi, phát hiện và hạn chế chi phí ngoài dự kiến.

---

### [Blog 3: API đã có AWS WAF, vì sao vẫn cần Throttling?](3.3-Blog3/)

- **Chủ đề:** AWS WAF, API Gateway, Rate Limiting & API Security
- **Tóm tắt nội dung:** Phân tích vai trò bổ trợ giữa AWS WAF và API Gateway Throttling trong việc lọc lưu lượng bất thường, giới hạn tốc độ request và bảo vệ AWS Lambda. Đồng thời đề cập đến rủi ro truy cập trực tiếp API Gateway và cách giám sát bằng Amazon CloudWatch.

---

### [Blog 4: Amazon Bedrock: Kiểm soát request và token usage trước khi chi phí tăng cao](3.4-Blog4/)

- **Chủ đề:** Amazon Bedrock, API Security, Token Usage & Cost Optimization
- **Tóm tắt nội dung:** Giới thiệu kiến trúc kiểm soát request và hạn mức token theo từng tenant bằng AWS WAF, API Gateway, Lambda và DynamoDB. Kết hợp CloudWatch, SNS, S3 và Athena để theo dõi, cảnh báo và phân tích mức sử dụng mô hình nhằm hạn chế chi phí ngoài dự kiến.
