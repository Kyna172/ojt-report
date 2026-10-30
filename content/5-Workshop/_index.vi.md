---
title: "Workshop"
date: 2025-08-11
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Đảm bảo truy cập Hybrid an toàn đến Amazon S3 bằng VPC Endpoints

#### Tổng quan bài thực hành

**AWS PrivateLink** cung cấp khả năng kết nối mạng riêng tư an toàn tới các dịch vụ của AWS từ môi trường Amazon VPC cũng như từ trung tâm dữ liệu nội bộ (On-Premises) mà hoàn toàn không để lộ lưu lượng truy cập ra ngoài mạng Internet công cộng.

Trong bài thực hành chuyên sâu này, chúng ta sẽ học cách thiết kế, cấu hình và kiểm thử các điểm cuối mạng ảo (VPC Endpoints) nhằm cho phép các ứng dụng kết nối trực tiếp đến dịch vụ Amazon S3 với mức độ cô lập mạng cao nhất, đáp ứng các tiêu chuẩn bảo mật khắt khe của doanh nghiệp.

Chúng ta sẽ tìm hiểu và triển khai hai loại VPC Endpoint chính:
* **Gateway VPC Endpoint:** Cho phép máy chủ trong VPC gửi lưu lượng tới Amazon S3 hoặc DynamoDB hoàn toàn qua dải IP nội bộ của AWS bằng cách cập nhật danh sách tiền tố trong bảng định tuyến Route Table (hoàn toàn miễn phí).
* **Interface VPC Endpoint (nền tảng AWS PrivateLink):** Cấp phát các card mạng ảo ENI mang địa chỉ IP riêng ngay trong Subnet của bạn. Đây là giải pháp bắt buộc để các máy chủ từ trung tâm dữ liệu On-Premises có thể truy cập S3 thông qua kênh kết nối mạng riêng ảo Site-to-Site VPN hoặc AWS Direct Connect.

---

#### Mục lục nội dung bài thực hành

1. [Tổng quan kiến trúc Workshop](5.1-Workshop-overview/)
2. [Các bước chuẩn bị & Khởi tạo Stack](5.2-Prerequiste/)
3. [Truy cập S3 từ Cloud VPC qua Gateway Endpoint](5.3-S3-vpc/)
4. [Truy cập S3 từ On-Premises qua Interface Endpoint](5.4-S3-onprem/)
5. [Thiết lập Endpoint Policy & Vành đai bảo mật dữ liệu](5.5-Policy/)
6. [Dọn dẹp tài nguyên & Tránh phát sinh chi phí](5.6-Cleanup/)
