---
title: "Blog 2"
date: 2026-11-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# ĐẶT AWS BUDGET 10 USD, VÌ SAO HÓA ĐƠN VẪN CÓ THỂ VƯỢT 10 USD?

**Bài viết đã chia sẻ trên cộng đồng AWS Study Group.**

**Link bài đăng:** [Xem bài viết trên Facebook](https://www.facebook.com/share/p/1FEBCbpDM7/)

## Nội dung bài viết

AWS Budgets là công cụ giúp theo dõi chi phí và gửi cảnh báo khi mức chi tiêu đạt ngưỡng đã thiết lập. Tuy nhiên, việc đặt ngân sách 10 USD không đồng nghĩa AWS sẽ tự động dừng các dịch vụ khi chi phí chạm mức này.

Để hạn chế chi phí ngoài dự kiến, người dùng cần hiểu sự khác biệt giữa cảnh báo ngân sách và các biện pháp kiểm soát chi phí thực tế.

### Các điểm chính cần nắm

- **AWS Budgets:** Theo dõi chi phí thực tế hoặc dự báo, hỗ trợ gửi cảnh báo qua email hoặc Amazon SNS khi đạt ngưỡng cấu hình.
- **Ngân sách không phải giới hạn chi tiêu cứng:** Các dịch vụ AWS vẫn có thể tiếp tục hoạt động và phát sinh chi phí sau khi vượt ngân sách.
- **Budgets Actions:** Cho phép áp dụng chính sách IAM hoặc thực hiện hành động đối với các EC2/RDS instance được chỉ định khi đạt ngưỡng ngân sách.
- **AWS Cost Anomaly Detection:** Sử dụng Machine Learning để phát hiện những biến động chi phí bất thường và gửi cảnh báo.
- **AWS Cost Explorer:** Hỗ trợ phân tích chi phí theo dịch vụ, Region hoặc loại sử dụng để xác định nguyên nhân phát sinh.
- **Độ trễ dữ liệu:** Thông tin chi phí không được cập nhật liên tục theo thời gian thực, vì vậy tổng chi phí thực tế có thể vượt ngưỡng trước khi cảnh báo được gửi đi.

### Ứng dụng thực tế

Đối với tài khoản học tập hoặc môi trường thử nghiệm, có thể kết hợp AWS Budgets, Cost Anomaly Detection, Cost Explorer và Budgets Actions để theo dõi ngân sách, phát hiện chi phí bất thường và triển khai các biện pháp kiểm soát phù hợp.

Điều quan trọng là AWS Budgets không phải cơ chế đảm bảo tài khoản sẽ không bao giờ bị tính phí vượt mức ngân sách đã đặt.

## Hình ảnh

<img width="1080" height="540" alt="image" src="https://github.com/user-attachments/assets/f7a62cc9-81d7-46e8-902a-afb7823ec83a" />

## Tài liệu tham khảo

- [AWS Documentation – Using AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/bcm-lite-use-budget.html)
- [AWS Documentation – Configuring Budget Actions](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-controls.html)
- [AWS Documentation – Cost Anomaly Detection](https://docs.aws.amazon.com/cost-management/latest/userguide/manage-ad.html)
