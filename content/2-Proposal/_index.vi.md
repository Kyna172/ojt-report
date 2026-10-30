---
title: "Bản đề xuất"
date: 2025-08-11
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Nền tảng quan trắc thời tiết IoT phục vụ nghiên cứu phòng Lab
## Giải pháp AWS Serverless hợp nhất cho giám sát dữ liệu thời gian thực

### 1. Tóm tắt điều hành
Dự án **IoT Weather Platform** được đề xuất và xây dựng nhằm phục vụ nhóm nghiên cứu *ITea Lab* tại TP. Hồ Chí Minh trong việc tự động hóa quá trình thu thập, trực quan hóa và phân tích dữ liệu vi khí hậu. Hệ thống hỗ trợ kết nối từ 5 trạm quan trắc ban đầu và sẵn sàng mở rộng lên 15 trạm, sử dụng thiết bị biên Raspberry Pi kết hợp các module cảm biến vi điều khiển ESP32 truyền dữ liệu qua giao thức MQTT.

Toàn bộ hệ thống phần mềm vận hành trên nền tảng AWS Serverless giúp hiển thị dữ liệu thời gian thực, lưu trữ hồ dữ liệu (Data Lake) phục vụ huấn luyện trí tuệ nhân tạo (AI), tiết kiệm tối đa chi phí vận hành và phân quyền truy cập an toàn cho các thành viên nghiên cứu thông qua Amazon Cognito.

---

### 2. Tuyên bố vấn đề & Mục tiêu giải pháp
#### Bài toán thực tế
Trước đây, các trạm quan trắc thủ công tại phòng lab đòi hỏi nghiên cứu sinh phải đến tận nơi tháo thẻ nhớ SD để lấy dữ liệu định kỳ. Quy trình này tốn nhiều công sức, dễ gây thất lạc dữ liệu khi thiết bị gặp sự cố. Mặt khác, các nền tảng IoT thương mại đóng gói sẵn thường tính phí duy trì đắt đỏ và không cho phép tùy biến luồng dữ liệu theo đúng yêu cầu học thuật.

#### Giải pháp đề xuất
Hệ thống giải quyết triệt để vấn đề trên thông qua chuỗi dịch vụ đám mây AWS:
* **Thu thập (Ingestion):** Dịch vụ **AWS IoT Core** tiếp nhận dữ liệu MQTT từ các trạm biên với chứng chỉ bảo mật mã hóa X.509.
* **Lưu trữ & Hồ dữ liệu:** Toàn bộ bản tin JSON thô được đưa trực tiếp vào **Amazon S3 Data Lake**.
* **Xử lý & Chuyển đổi ETL:** **AWS Glue Crawlers** tự động phát hiện cấu trúc schema và chạy các tiến trình **AWS Glue ETL** chuyển đổi dữ liệu sang định dạng cột nén Apache Parquet tối ưu cho truy vấn phân tích.
* **Tầng API & Dịch vụ:** **AWS Lambda** và **Amazon API Gateway** cung cấp các REST API phi máy chủ tốc độ cao phục vụ ứng dụng web.
* **Giao diện bảng điều khiển:** Ứng dụng web viết bằng **Next.js** được triển khai trên **AWS Amplify**, mang lại trải nghiệm xem biểu đồ động thời gian thực mượt mà.
* **Bảo mật truy cập:** Phân quyền người dùng thông qua **Amazon Cognito**.

#### Lợi ích & Hoàn vốn đầu tư (ROI)
* **Tự động hóa 100%:** Chấm dứt hoàn toàn công việc sao chép thẻ nhớ thủ công, tiết kiệm hàng chục giờ lao động mỗi tháng.
* **Chi phí cực thấp:** Tận dụng AWS Free Tier và mô hình thanh toán theo nhu cầu thực tế của Serverless, chi phí đám mây chỉ khoảng **0,70 USD / tháng** (~8,40 USD / năm).
* **Giá trị nghiên cứu lâu dài:** Cung cấp kho dữ liệu sạch, liên tục làm đầu vào quý giá cho các đề tài nghiên cứu dự báo thời tiết bằng học máy (Machine Learning).

---

### 3. Kiến trúc giải pháp kỹ thuật

Hệ thống được chia làm hai phân tầng chính: Phân tầng thiết bị biên (Edge) và Phân tầng nền tảng đám mây (Cloud Platform):

![Kiến trúc trạm quan trắc biên IoT](/images/2-Proposal/edge_architecture.jpeg)

![Kiến trúc nền tảng Serverless trên AWS](/images/2-Proposal/platform_architecture.jpeg)

#### Các dịch vụ AWS cốt lõi:
* **AWS IoT Core:** Cổng kết nối và điều phối tin nhắn MQTT hai chiều có xác thực chứng chỉ.
* **AWS Lambda:** Thực thi mã nguồn xử lý logic nghiệp vụ không cần máy chủ.
* **Amazon API Gateway:** Cổng tiếp nhận và phân phối các yêu cầu REST API.
* **Amazon S3:** Kho lưu trữ bền vững cho dữ liệu thô và dữ liệu phân tích Parquet.
* **AWS Glue:** Trích xuất, lập danh mục schema và chuyển đổi dữ liệu hàng loạt (ETL).
* **AWS Amplify:** Nền tảng lưu trữ và tự động build ứng dụng Next.js.
* **Amazon Cognito:** Quản lý tài khoản đăng nhập và cấp token bảo mật.

---

### 4. Lộ trình triển khai kỹ thuật

1. **Giai đoạn 1: Thiết kế lý thuyết & Thử nghiệm phần cứng (Trước thực tập)**  
   Nghiên cứu sơ đồ mạch cảm biến ESP32, căn chỉnh các đầu dò nhiệt độ, độ ẩm, áp suất và phác thảo kiến trúc đám mây mục tiêu.
2. **Giai đoạn 2: Tính toán chi phí & Đánh giá tính khả thi (Tháng 1)**  
   Sử dụng công cụ AWS Pricing Calculator để mô phỏng chính xác dung lượng mạng và chi phí từng dịch vụ, đảm bảo ngân sách duy trì dưới 1 USD/tháng.
3. **Giai đoạn 3: Hiện thực hóa hạ tầng & Tích hợp chuỗi dịch vụ (Tháng 2)**  
   Thiết lập các Rule trên IoT Core, tạo bucket S3, viết script chuyển đổi trên Glue và xây dựng các hàm Lambda bằng mã nguồn IaC.
4. **Giai đoạn 4: Hoàn thiện bảng điều khiển web & Kiểm thử thực địa (Tháng 3)**  
   Lập trình giao diện Next.js trên Amplify, kết nối dữ liệu thật từ trạm quan trắc và tối ưu cơ chế lưu đệm khi mất mạng Wi-Fi.

---

### 5. Kế hoạch mốc tiến độ (Milestones)
* **Mốc 1:** Nạp firmware cảm biến ổn định, truyền tin nhắn MQTT lên AWS IoT Core thành công.
* **Mốc 2:** Hoàn thành luồng S3 Data Lake và tiến trình tự động Glue ETL.
* **Mốc 3:** Đăng nhập hệ thống qua Cognito và xem biểu đồ thời gian thực trên Amplify.
* **Mốc 4:** Kiểm thử tải toàn diện và hoàn thiện hồ sơ nghiệm thu kỹ thuật.

---

### 6. Dự toán ngân sách thực tế

Bảng ước tính chi phí hàng tháng được lập trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01):

| Dịch vụ AWS | Quy mô sử dụng dự kiến hàng tháng | Chi phí ước tính (USD) |
| :--- | :--- | :--- |
| **AWS IoT Core** | 5 trạm gửi tin, ~45.000 bản tin MQTT/tháng | $0.08 |
| **Amazon S3** | 6 GB lưu trữ, ~2.100 lượt gọi PUT/GET | $0.15 |
| **AWS Lambda** | 1.000 lượt thực thi, 512 MB bộ nhớ | $0.00 (Free Tier) |
| **Amazon API Gateway** | 2.000 lượt gọi REST request | $0.01 |
| **AWS Glue** | 1 Crawler + 2 DPU-giờ chạy ETL định kỳ | $0.09 |
| **AWS Amplify** | Hosting ứng dụng web tĩnh & băng thông mạng | $0.35 |
| **Băng thông mạng ra ngoài** | 1 GB dữ liệu truyền tải | $0.02 |
| **Tổng chi phí vận hành Cloud** | **Tổng ước tính** | **~$0.70 USD / tháng** |

*Chi phí phần cứng:* Tận dụng lại các linh kiện có sẵn tại phòng lab (ESP32, cảm biến môi trường, Raspberry Pi 5 trị giá ~265 USD), không tốn thêm ngân sách mua sắm mới.

---

### 7. Đánh giá rủi ro & Kế hoạch phòng ngừa

* **Rủi ro gián đoạn mạng Wi-Fi tại trạm biên:**  
  *Biện pháp:* Ứng dụng chạy trên Raspberry Pi được đóng gói qua Docker, có sẵn cơ sở dữ liệu đệm SQLite nội bộ. Khi mất mạng, dữ liệu tạm lưu trên thẻ nhớ; khi có mạng trở lại, hệ thống tự động đẩy bù các bản tin còn thiếu lên IoT Core.
* **Rủi ro lỗi cảm biến do thời tiết khắc nghiệt:**  
  *Biện pháp:* Lập trình cơ chế Heartbeat định kỳ kiểm tra tình trạng cảm biến, trang bị sẵn các linh kiện thay thế nhanh tại chỗ.
* **Rủi ro chi phí điện toán đám mây phát sinh ngoài ý muốn:**  
  *Biện pháp:* Thiết lập AWS Budgets gửi email cảnh báo ngay khi chi phí vượt 2 USD/tháng và giới hạn số lượng tác vụ đồng thời của Lambda.

---

### 8. Kết quả kỳ vọng & Giá trị dự án
* **Vận hành tự động:** Hệ thống giám sát khí hậu hoạt động liên tục 24/7 không cần can thiệp tay.
* **Tài sản học thuật:** Cung cấp bộ dữ liệu thời tiết chất lượng cao, định dạng chuẩn cho các đề tài nghiên cứu khoa học và đồ án tốt nghiệp của sinh viên khóa sau.
