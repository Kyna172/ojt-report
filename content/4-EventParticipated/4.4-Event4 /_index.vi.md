---
title: "First Cloud AI Journey: Weekly Meet Up 24/10"
date: 2026-10-24
weight: 1
chapter: false
pre: "<b> 4.4. </b>"
---

## Video sự kiện: [Xem trên YouTube](https://www.youtube.com/watch?v=dJiP5890kTg)

---
title: "First Cloud AI Journey: Weekly Meet Up 24/10"
date: 2026-10-24
weight: 1
chapter: false
pre: "  4.4.  "
---

### Mục đích của sự kiện

* Cập nhật kiến thức chuyên sâu và trải nghiệm thực tế về công nghệ Cloud & AI Agent từ các Tech Lead và kỹ sư doanh nghiệp.
* Tìm hiểu các giải pháp tối ưu hóa kiến trúc hạ tầng, bảo mật an toàn thông tin và quản trị chi phí trên AWS.
* Tiếp cận cách xây dựng và đưa các ứng dụng AI Agent (Voice AI, Pentest Agent, Agent Framework) vào môi trường production.
* Giao lưu, kết nối và học hỏi kinh nghiệm từ cộng đồng AWS Student Builder Group và các chuyên gia công nghệ.

### Danh sách diễn giả

* **Anh Kiệt Trần** - Revve AI
* **Anh Long Huỳnh** - Styl Solution
* **Anh Thịnh Nguyễn** - Styl Solution
* **Anh Xuân An** - Leader AWS Student Builder Group HCMUTE
* **Anh Khoa Kiều** - Tech Lead ACB
* **Anh Nghi Danh** - AWS Community Builder

### Nội dung nổi bật

#### Session 1: Hear, Think, Speak - Building a Vietnamese Voice-AI Contact Center on AWS

* **Kiến trúc Voice AI**: Giải pháp tối ưu hóa đường truyền và xử lý để giảm độ trễ cuộc gọi xuống còn ~1.8s, giúp tương tác giọng nói mượt mà và tự nhiên.
* **Live Demo thực tế**: Trải nghiệm hệ thống AI phỏng vấn sơ tuyển tự động vị trí Cloud Engineer hoàn toàn bằng tiếng Việt với phản hồi linh hoạt.

#### Session 2: AWS Resource Access Manager (RAM)

* **Chia sẻ tài nguyên an toàn**: Phương pháp chia sẻ tài nguyên giữa các tài khoản độc lập trong cùng AWS Organization giúp tối ưu chi phí và quy hoạch quản trị mạng tập trung.
* **Quản trị truy cập đa lớp**: Kết hợp chặt chẽ giữa IAM policy (quyền cấp phát) và SCP (Service Control Policies) để thiết lập trần quyền hạn cứng, chống vượt quyền.

#### Session 3: AWS Pentest with AWS Continuum / Security Agent

* **Đánh giá an toàn hạ tầng từ sớm**: Tích hợp tự động kiểm tra mã nguồn IaC (Terraform) trực tiếp vào luồng GitLab/GitHub Pull Request để phát hiện lỗ hổng cấu hình trước khi merge.
* **Pentest tự động với Security Agent**: Mô phỏng Security Agent đóng vai người dùng thực để quét và thực hiện pentest tự động trên các môi trường SIT/UAT trước khi triển khai chính thức.

#### Session 4: Amazon Bedrock AgentCore

* **Agent Runtime**: Tối ưu chi phí vận hành bằng cách chạy MicroVM trên hạ tầng EC2 Spot cho các tác vụ xử lý của Agent.
* **Hệ thống Memory phân tầng**: Mô hình phân chia Short-term memory (đồng bộ theo phiên làm việc) và Long-term memory (bất đồng bộ) giúp Agent duy trì ngữ cảnh người dùng sâu sắc và chính xác.

#### Session 5: Kiro Crew - AI Agent 24/7 Review Code & System Monitoring

* **Tự động hóa tác vụ**: Xây dựng AI Agent hoạt động 24/7 hỗ trợ review code và kiểm tra trạng thái vận hành hệ thống.
* **Tạo Artifacts linh hoạt**: Cơ sở để Agent tự động thu thập dữ liệu việc làm thực tế và trực quan hóa thành biểu đồ ngay trong giao diện chat.
* **Quản trị Context Window & Token**: Cơ chế *Auto Compact* tự động nén ngữ cảnh khi dung lượng chạm ngưỡng 70–90%, kết hợp tính năng *Break down context* để theo dõi chi tiết mức tiêu thụ token của từng thành phần.
* **Bảo mật & Quản lý Memory**: Thiết lập lớp chặn Guardrails ngăn AI tự ý thực thi các lệnh nguy hiểm (xóa hạ tầng, làm rò rỉ secret/credential) và dọn dẹp các vùng nhớ cũ để kiểm soát chi phí.

### Những gì học được

#### Tư duy thiết kế & kiến trúc

* **Tối ưu hóa độ trễ (Latency Management)**: Bài học thực tế về việc cân bằng giữa độ chính xác của mô hình AI và tốc độ phản hồi real-time trong các bài toán Voice AI.
* **Bảo mật Shift-Left**: Đưa khâu kiểm tra an toàn thông tin (IaC review, pentest tự động) vào sớm ngay trong pipeline CI/CD thay vì đợi đến khi hệ thống đã lên production.
* **Quản trị vòng đời AI Agent**: Hiểu rõ tầm quan trọng của việc quản lý bộ nhớ (Memory), ngữ cảnh (Context Window) và chi phí tài nguyên (EC2 Spot, Token consumption) khi đưa Agent vào vận hành thực tế.

#### Kỹ thuật & bảo mật hạ tầng

* **Nguyên tắc Privilege Boundaries**: Sự kết hợp giữa IAM Policy và SCP trên AWS RAM giúp đảm bảo nguyên tắc quyền tối thiểu (Least Privilege) trên quy mô doanh nghiệp.
* **An toàn cho Generative AI**: Kỹ thuật thiết lập lớp bảo vệ (Guardrails) cho AI Agent nhằm kiểm soát hành vi, tránh việc thi hành lệnh phá hoại hạ tầng hoặc rò rỉ dữ liệu nhạy cảm.

### Ứng dụng vào công việc

* **Tích hợp Security Scan vào CI/CD**: Nghiên cứu đưa các công cụ kiểm tra IaC (Terraform review) vào luồng GitHub/GitLab PR cho các bài tập hoặc dự án cá nhân.
* **Áp dụng tư duy quản trị Context & Memory**: Áp dụng cơ chế nén ngữ cảnh và phân tầng bộ nhớ khi phát triển các ứng dụng chatbot hoặc tích hợp LLM API.
* **Thực hành quản lý phân quyền AWS**: Thử nghiệm phân chia tài khoản AWS Organization và cấu hình AWS RAM cùng SCP để hiểu sâu hơn về kiến trúc Cloud Security.
* **Chủ động kết nối & học hỏi**: Tăng cường trao đổi, học hỏi kinh nghiệm từ các anh chị đi trước và đóng góp tích cực hơn trong các hoạt động cộng đồng công nghệ.

### Trải nghiệm trong event

Buổi **Meet Up First Cloud AI Journey (24/10/2026)** tại lầu 26 Bitexco Financial Tower là một buổi học hỏi thực sự chất lượng, đem lại nhiều giá trị "chất xám" thực tế từ các chuyên gia doanh nghiệp.

#### Học hỏi từ các diễn giả & bài toán thực tế

* Ấn tượng mạnh với phần **Live Demo phỏng vấn bằng Voice AI** của Revve AI và cách các diễn giả giải quyết bài toán độ trễ ~1.8s.
* Tiếp thu được nhiều góc nhìn thực chiến về quản trị hạ tầng từ Styl Solution và kinh nghiệm triển khai AgentCore, Kiro Crew từ HCMUTE và ACB.

#### Trải nghiệm kỹ thuật & định hướng bản thân

* Thu nhận thêm nhiều bài học về việc quản trị token, chống phình chi phí khi chạy AI Agent 24/7 và cách cài đặt các lớp Guardrail bảo mật.
* Nhận ra khoảng cách giữa lý thuyết và thực tế doanh nghiệp, từ đó tạo động lực lớn để tiếp tục chủ động kết nối, trau dồi và nâng cao kỹ năng chuyên môn trên "hành trình lên mây".
> Tổng thể, 5 session trong sự kiện không chỉ cập nhật những công nghệ tiên tiến nhất về Cloud & AI Agent mà còn truyền nguồn năng lượng tích cực, giúp định hình rõ ràng hơn con đường phát triển kỹ thuật trong tương lai.

#### Một số hình ảnh khi tham gia sự kiện

<img width="960" height="640" alt="1793025824003_186912018913895205_6518061436599146441_cf574709f652a44a0bc22fed5a6ad8d0" src="https://github.com/user-attachments/assets/9c65fb36-cd86-46c1-ac11-ae66b3d72590" />

<img width="960" height="640" alt="1794412043999_186912018913895205_6518061436599146441_2d19283ebe987e54d77a9bae3987998f" src="https://github.com/user-attachments/assets/d871db56-543c-4f25-a6ca-9eefd52fba25" />

<img width="1280" height="960" alt="1793025824061_186912018913895205_6518061436599146441_aafdd8d9c94a05a45635d15d86b1ab0d" src="https://github.com/user-attachments/assets/388cbc25-83d5-4e0e-a220-391f3a8be7b1" />
