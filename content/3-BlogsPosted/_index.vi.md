---
title: "Các bài blogs đã đăng"
date: 2025-08-11
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# Các bài viết kỹ thuật đã chia sẻ tới cộng đồng

Trong suốt thời gian thực tập tại chương trình **First Cloud AI Journey (FCAJ)**, em đã tích cực tham gia nghiên cứu, đúc kết kinh nghiệm thực chiến và chia sẻ các bài viết chuyên môn trên cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Các bài viết tập trung giải quyết những vấn đề thực tế thường gặp khi xây dựng hạ tầng trên AWS, từ bảo mật phân quyền Kubernetes đến tối ưu mạng phân phối nội dung và kiến trúc phi máy chủ.

Dưới đây là 3 bài viết kỹ thuật tiêu biểu đã được đăng tải:

---

### [Blog 1: Bảo mật đặc quyền tối thiểu với Amazon EKS Pod Identity và Session Policies](3.1-blog1/)
* **Chủ đề:** Bảo mật hạ tầng Kubernetes & Quản lý danh tính đám mây
* **Tóm tắt nội dung:** Đi sâu phân tích tính năng Amazon EKS Pod Identity kết hợp Session Policies giúp thu hẹp quyền IAM linh hoạt cho từng Pod riêng lẻ mà không cần phải khởi tạo hàng loạt IAM Role cồng kềnh, giải quyết triệt để bài toán chạm hạn mức IAM Quota trong các cụm Kubernetes quy mô lớn.

---

### [Blog 2: Tối ưu hiệu năng và bảo mật lưu trữ Web tĩnh với S3 và CloudFront Origin Access Control (OAC)](3.2-blog2/)
* **Chủ đề:** Tối ưu hóa website, Bộ nhớ đệm biên & An toàn thông tin
* **Tóm tắt nội dung:** Hướng dẫn chi tiết cách triển khai website tĩnh an toàn tuyệt đối: Đóng kín S3 Bucket không mở quyền public trực tiếp, bắt buộc mọi lượt truy cập phải đi qua mạng lưới trạm biên toàn cầu của CloudFront nhờ cơ chế xác thực Origin Access Control (OAC).

---

### [Blog 3: Xây dựng đường ống xử lý ảnh tự động hướng sự kiện với S3, Lambda và DynamoDB](3.3-blog3/)
* **Chủ đề:** Kiến trúc phi máy chủ Serverless & Xử lý bất đồng bộ
* **Tóm tắt nội dung:** Thiết kế kiến trúc Serverless xử lý đa phương tiện tự động: Khi người dùng tải ảnh lên S3, dịch vụ sẽ tự động bắn sự kiện kích hoạt hàm AWS Lambda để nén ảnh, tạo thumbnail và lưu trữ thông tin kích thước, định dạng vào cơ sở dữ liệu DynamoDB trong chớp mắt.
