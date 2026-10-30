---
title: "Sự kiện 2"
date: 2025-08-11
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Báo cáo tổng kết: Ngày hội công nghệ "AWS Community Day Vietnam 2025"

### Thông tin sự kiện
* **Tên sự kiện:** AWS Community Day Vietnam 2025
* **Thời gian:** 08:30 – 16:30, Ngày 20/09/2025
* **Địa điểm:** Trung tâm Hội nghị Grand Palace, Quận Tân Bình, TP. Hồ Chí Minh
* **Vai trò tham dự:** Khách mời kỹ thuật & Tình nguyện viên hỗ trợ cộng đồng sinh viên

---

### Quy mô & Không khí sự kiện
**AWS Community Day** là sự kiện công nghệ đám mây thường niên lớn nhất do chính cộng đồng các kỹ sư AWS User Group tại Việt Nam tổ chức. Năm 2025, ngày hội quy tụ hơn **600+ kỹ sư Cloud, chuyên gia kiến trúc giải pháp, các lãnh đạo công nghệ (CTO/VP of Engineering) và các bạn sinh viên đam mê công nghệ**, với nhiều phòng hội thảo chuyên đề song song xoay quanh Generative AI, DevOps, Container và An toàn thông tin.

---

### Các phiên hội thảo kỹ thuật ấn tượng nhất

#### 1. Phiên toàn thể: Ứng dụng Generative AI cho Doanh nghiệp với Amazon Bedrock
* **Diễn giả:** Các chuyên gia đạt danh hiệu AWS Community Hero và Kiến trúc sư giải pháp doanh nghiệp.
* **Bài học cốt lõi:**
  * Thay vì tự bỏ hàng triệu USD để huấn luyện mô hình ngôn ngữ lớn từ đầu, các doanh nghiệp đang tạo ra giá trị đột phá nhanh chóng bằng cách khai thác các Foundation Model hàng đầu thế giới (Claude 3.5 Sonnet, Llama 3, Amazon Titan) qua **Amazon Bedrock**.
  * Kỹ thuật tìm kiếm tăng cường truy xuất **RAG (Retrieval-Augmented Generation)** kết hợp giữa Amazon OpenSearch Serverless hoặc tiện ích mở rộng pgvector trên Amazon RDS PostgreSQL để AI trả lời chính xác dựa trên tài liệu nghiệp vụ nội bộ của công ty.
  * Thiết lập hàng rào bảo vệ **Guardrails for Amazon Bedrock** để tự động lọc bỏ thông tin nhạy cảm (PII), chống lộ dữ liệu bí mật và ngăn chặn các câu lệnh prompt nguy hại.

#### 2. Chuyên đề chuyên sâu: Tối ưu chi phí hạ tầng Kubernetes trên Amazon EKS
* **Diễn giả:** Trưởng phòng DevOps tại một kỳ lân công nghệ khu vực Đông Nam Á.
* **Bài học cốt lõi:**
  * Xu hướng chuyển dịch từ công cụ Cluster Autoscaler cổ điển sang **Karpenter** - bộ tự động cấp phát node máy chủ mã nguồn mở cực nhanh do AWS phát triển.
  * Karpenter chỉ mất vài mili-giây để phân tích các Pod đang chờ cấp phát và tự động chọn loại máy chủ EC2 Spot có giá rẻ nhất, giúp cắt giảm tới hơn 45% chi phí máy chủ cụm EKS.
  * Tận dụng dòng chip thế hệ mới AWS Graviton kiến trúc ARM (`c7g`, `m7g`) để tối ưu tỷ lệ hiệu năng trên giá thành (Price-to-Performance).

#### 3. Chuyên đề An toàn thông tin: Kiến trúc Zero-Trust trên nền tảng AWS
* **Diễn giả:** Chuyên gia tư vấn an ninh mạng cao cấp AWS.
* **Bài học cốt lõi:**
  * Triết lý "Không bao giờ tin tưởng, luôn luôn xác thực": Chuyển từ việc bảo vệ theo chu vi tường lửa cứng nhắc sang xác thực định danh chi tiết ở từng tầng giao dịch.
  * Ứng dụng AWS IAM Roles Anywhere, AWS PrivateLink và hệ thống phát hiện mối đe dọa thông minh Amazon GuardDuty có khả năng tự động cô lập máy chủ nhiễm mã độc bằng hàm Lambda.

---

### Trải nghiệm thực tế & Hoạt động tình nguyện của sinh viên

#### Hoạt động hỗ trợ sự kiện
Bên cạnh việc lắng nghe các bài thuyết trình chuyên môn, em rất vinh dự được cùng các anh chị trong ban tổ chức FCAJ tham gia hỗ trợ bàn thông tin: Hướng dẫn check-in mã QR cho khách tham dự, phát tài liệu hướng dẫn các phòng hội thảo và chia sẻ những câu chuyện thực tế về kỳ thực tập Cloud của mình cho các bạn sinh viên khóa dưới.

#### Trải nghiệm các gian hàng công nghệ tương tác
Tại khu vực triển lãm công nghệ, em đã có dịp trực tiếp trải nghiệm:
* Mô hình camera thị giác máy tính chạy ở thiết bị biên kết hợp AWS IoT Greengrass nhận diện lỗi sản phẩm trong nhà máy sản xuất.
* Trải nghiệm ứng dụng trợ lý ảo AI hỏi đáp thông minh kết nối với dữ liệu tài liệu kỹ thuật của AWS.

#### Mở rộng mạng lưới kết nối nghề nghiệp (Networking)
Khoảnh khắc tuyệt vời nhất là được trực tiếp trò chuyện cùng các anh chị kỹ sư trưởng (Lead DevOps) trong giờ ăn trưa. Các anh chị đã chia sẻ rất cởi mở về lộ trình phát triển nghề nghiệp: Không nên chỉ học vẹt các chứng chỉ đám mây, mà điều nhà tuyển dụng tìm kiếm nhất ở một sinh viên mới ra trường là sự am hiểu sâu sắc về mạng, hệ điều hành Linux và khả năng tự tay làm các dự án thực tế kèm theo việc viết blog chia sẻ kiến thức.

---

### Lời kết
Tham gia AWS Community Day Vietnam 2025 là một cột mốc đáng nhớ trong kỳ thực tập của em. Sự kiện không chỉ tiếp thêm cho em nguồn cảm hứng kỹ thuật dồi dào mà còn giúp em củng cố vững chắc quyết tâm theo đuổi định hướng trở thành một Kỹ sư Kiến trúc giải pháp Đám mây (Cloud Solutions Architect) trong tương lai.
