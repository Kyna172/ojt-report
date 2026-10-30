---
title: "Sự kiện 1"
date: 2025-08-11
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Báo cáo tổng kết: Hội thảo "Hiện đại hóa Ứng dụng & Cơ sở dữ liệu ứng dụng GenAI"

### Thông tin sự kiện
* **Tên sự kiện:** GenAI-powered App-DB Modernization Workshop
* **Thời gian:** 09:00 – 17:00, Ngày 13/08/2025
* **Địa điểm:** Tầng 26, Bitexco Financial Tower, Quận 1, TP. Hồ Chí Minh
* **Vai trò tham dự:** Người tham dự (Attendee)

---

### Diễn giả khách mời
* **Jignesh Shah** – Giám đốc mảng Cơ sở dữ liệu mã nguồn mở tại AWS
* **Erica Liu** – Chuyên gia cao cấp chiến lược thị trường Hiện đại hóa ứng dụng tại AWS
* **Fabrianne Effendi** – Chuyên gia Kiến trúc giải pháp Serverless tại AWS

---

### Các nội dung trọng tâm tiếp thu được

#### 1. Nhận diện các điểm nghẽn của kiến trúc nguyên khối cũ (Monolith)
* **Chu kỳ phát hành chậm chạp:** Mã nguồn dính chặt vào nhau khiến việc chỉnh sửa một tính năng nhỏ cũng tiềm ẩn rủi ro hỏng toàn bộ hệ thống, kéo dài thời gian kiểm thử và đưa sản phẩm ra thị trường.
* **Độ ổn định mong manh:** Một lỗi tràn bộ nhớ ở phân hệ xuất báo cáo có thể kéo theo sập luôn luồng thanh toán cốt lõi.
* **Lãng phí chi phí phần cứng:** Không thể co giãn riêng lẻ các module đang bị quá tải, buộc doanh nghiệp phải nâng cấp toàn bộ cụm máy chủ đắt đỏ.

#### 2. Phương pháp thiết kế hướng miền (Domain-Driven Design - DDD)
* **Kỹ thuật Event Storming:** Mô hình hóa các quy trình nghiệp vụ thực tế thành các chuỗi sự kiện theo trục thời gian trước khi bắt tay vào gõ dòng code nào.
* **Ngữ cảnh giới hạn (Bounded Context):** Xác định rõ ranh giới tự trị của từng phân hệ, mỗi dịch vụ tự quản lý cơ sở dữ liệu riêng của mình, chỉ giao tiếp qua giao diện API rõ ràng.
* **Bản đồ ngữ cảnh (Context Mapping):** Áp dụng các mẫu tích hợp giảm thiểu phụ thuộc (Anti-Corruption Layer, Shared Kernel).

#### 3. Chuyển dịch sang kiến trúc hướng sự kiện (EDA)
* Thay thế cơ chế gọi API đồng bộ nối tiếp nhau bằng hàng đợi tin nhắn và kênh truyền phát (Amazon EventBridge, Amazon SNS/SQS).
* Phân tích ưu nhược điểm giữa các mô hình: Đăng ký/Nhận tin (Pub/Sub), Điểm - Điểm (Point-to-point) và Luồng dữ liệu liên tục (Streaming).

#### 4. Phổ tiến hóa của hạ tầng điện toán đám mây
* Đi từ máy ảo truyền thống (Amazon EC2) -> Container đóng gói (Amazon ECS/EKS) -> Phi máy chủ (AWS Fargate & AWS Lambda).
* Lợi ích vượt trội của Serverless: Hoàn toàn không mất công bảo trì hệ điều hành, tự động co giãn theo lưu lượng truy cập và chỉ tính tiền khi có request xử lý.

#### 5. Đột phá cùng trợ lý AI - Amazon Q Developer
* Ứng dụng Generative AI ngay trong IDE để giải thích mã nguồn cũ, tự động sinh Unit Test và nâng cấp các phiên bản runtime cổ điển (Java 8 lên Java 17/21) chỉ trong vài phút.
* Hỗ trợ tách các Stored Procedure phức tạp trong cơ sở dữ liệu thành các vi dịch vụ hiện đại.

---

### Cảm nhận thực tế và Giá trị ứng dụng cho bản thân

#### Thay đổi tư duy thiết kế hệ thống
Buổi hội thảo giúp em vỡ ra một bài học rất lớn: Kiến trúc phần mềm đỉnh cao không phải là chạy theo các công nghệ thời thượng nhất, mà là phải xuất phát từ bài toán nghiệp vụ kinh doanh (Business-First). Mọi quyết định kỹ thuật đều phải phục vụ cho mục tiêu giúp doanh nghiệp vận hành linh hoạt và an toàn hơn.

#### Ứng dụng trực tiếp vào đề tài thực tập
* Sau buổi học, em đã áp dụng ngay tư duy hướng sự kiện vào bản đề xuất kiến trúc (Proposal) của mình: Tách biệt hoàn toàn luồng thu thập dữ liệu cảm biến IoT và luồng xử lý phân tích thông qua sự kiện S3 Event thay vì gọi trực tiếp.
* Em bắt đầu cài đặt và sử dụng Amazon Q Developer vào quá trình học tập, giúp việc tra cứu cú pháp AWS CDK và viết test nhanh hơn đáng kể.

#### Cơ hội giao lưu học hỏi
Được trực tiếp lắng nghe và đặt câu hỏi với các chuyên gia Kiến trúc giải pháp hàng đầu của AWS tại Việt Nam trong giờ giải lao là một trải nghiệm truyền cảm hứng mạnh mẽ, giúp em hình dung rõ ràng hơn về con đường phát triển sự nghiệp của một Cloud Solutions Architect chuyên nghiệp.
