---
title: "Blog 1"
date: 2026-11-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# 5 BƯỚC QUẢN LÝ CHI PHÍ AMAZON BEDROCK: KHÔNG CHỈ ĐƠN GIẢN LÀ GIẢM SỐ LƯỢNG TOKEN

**Bài viết đã chia sẻ trên cộng đồng AWS Study Group.**

**Link bài đăng:** [Xem bài viết trên Facebook](https://www.facebook.com/share/p/19UsES7evm/)

## Nội dung bài viết

Khi triển khai ứng dụng Generative AI với Amazon Bedrock, chi phí không chỉ phụ thuộc vào số lượng token và giá của từng mô hình. Việc xác định nguồn phát sinh chi phí, theo dõi mức sử dụng và thiết lập các biện pháp kiểm soát cũng đóng vai trò quan trọng.

AWS Machine Learning Blog giới thiệu quy trình quản lý chi phí Amazon Bedrock gồm **5 bước**, giúp doanh nghiệp chủ động theo dõi, kiểm soát và tối ưu chi phí trong quá trình vận hành.

### Các điểm chính cần nắm

- **1. Xác định chi phí:** Sử dụng AWS Cost and Usage Report (CUR 2.0), IAM tags và AWS Cost Explorer để phân tích chi phí theo người dùng, nhóm hoặc ứng dụng.
- **2. Theo dõi mức sử dụng:** Kích hoạt Model Invocation Logging để ghi nhận các lần gọi mô hình, phân tích token usage thông qua Amazon CloudWatch Logs hoặc Amazon S3.
- **3. Kiểm soát ngân sách:** Kết hợp AWS Budgets để cảnh báo, IAM và tự động hóa để hạn chế quyền truy cập, hoặc triển khai Gateway nhằm kiểm soát yêu cầu trước khi gọi mô hình.
- **4. Tối ưu chi phí:** Sử dụng Intelligent Prompt Routing, Prompt Caching và giới hạn token phù hợp để giảm tài nguyên tiêu thụ không cần thiết.
- **5. Đánh giá và cải thiện:** Theo dõi mức sử dụng mô hình, request thất bại và hiệu quả Prompt Caching để liên tục điều chỉnh chính sách quản lý chi phí.

### Ứng dụng thực tế

Quy trình này phù hợp với các ứng dụng Generative AI cần quản lý chi phí theo từng nhóm người dùng hoặc workload, đặc biệt khi số lượng request và mức tiêu thụ token tăng theo thời gian.

Thay vì chỉ kiểm tra hóa đơn cuối tháng, doanh nghiệp có thể kết hợp dữ liệu usage, cảnh báo ngân sách và các biện pháp tối ưu để chủ động kiểm soát chi phí Amazon Bedrock.

## Hình ảnh

<img width="1600" height="402" alt="Sơ đồ 5 bước quản lý chi phí Amazon Bedrock" src="https://github.com/user-attachments/assets/e2ab06fc-5b89-4b5e-afc2-5c18ee98af38" />

## Tài liệu tham khảo

AWS Machine Learning Blog – *Managing Amazon Bedrock costs end to end: A playbook for FinOps and platform teams* (30/10/2026).

[Đọc bài viết gốc trên AWS](https://aws.amazon.com/vi/blogs/machine-learning/managing-amazon-bedrock-costs-end-to-end-a-playbook-for-finops-and-platform-teams/)
