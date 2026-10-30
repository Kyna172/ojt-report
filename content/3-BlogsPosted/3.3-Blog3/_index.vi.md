---
title: "Blog 3"
date: 2025-08-11
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Xây dựng đường ống xử lý ảnh tự động hướng sự kiện với S3, Lambda và DynamoDB

### Bối cảnh thực tế: Vấn đề xử lý ảnh nặng nề
Hầu hết các dự án web hiện nay (từ mạng xã hội, sàn thương mại điện tử đến web blog cá nhân) đều có tính năng cho phép người dùng đăng ảnh đại diện hoặc ảnh sản phẩm. Những bức ảnh này thường có dung lượng rất lớn (5MB - 15MB) với độ phân giải cao.

Nếu backend chính của bạn (chạy trên Node.js, Spring Boot hay Django) trực tiếp gánh tác vụ giải nén, resize ảnh và lưu đĩa theo kiểu đồng bộ (Synchronous):
* Tiến trình máy chủ sẽ bị nghẽn (block CPU) trong lúc xử lý ảnh nặng.
* Người dùng phải chờ đợi xoay vòng rất lâu để nhận phản hồi, gây trải nghiệm tệ.
* Khi có nhiều người cùng upload ảnh một lúc, máy chủ rất dễ bị sập vì cạn kiệt RAM.

Giải pháp chuẩn kiến trúc đám mây hiện đại là tách rời (decouple) việc nhận ảnh và xử lý ảnh thông qua **mô hình xử lý bất đồng bộ hướng sự kiện (Event-Driven Architecture)**.

---

### Mô hình kiến trúc giải pháp

```
[ Người dùng tải ảnh lên ]
             |
             v
[ Amazon S3 (Bucket Ảnh Gốc) ]
             | (Sự kiện s3:ObjectCreated:*)
             v
[ Hàm AWS Lambda (Resize Ảnh) ]
       |                       |
       | (Lưu ảnh thumbnail)   | (Lưu metadata)
       v                       v
[ Amazon S3 (Bucket Đã Xử Lý) ]  [ Amazon DynamoDB ]
```

1. Ứng dụng web tải trực tiếp file ảnh gốc lên **S3 Bucket Ảnh Gốc** (sử dụng cơ chế S3 Presigned URL để không làm nặng máy chủ backend).
2. Ngay khi file vừa cập bến, S3 tự động bắn một sự kiện thông báo `ObjectCreated` sang **AWS Lambda**.
3. Hàm Lambda tự động khởi động, đọc luồng dữ liệu ảnh, dùng thư viện `Pillow` để resize ảnh về kích thước chuẩn (ví dụ 300x300 px) và lưu file nén sang **S3 Bucket Đã Xử Lý**.
4. Đồng thời, Lambda ghi lại một bản ghi thông tin (kích thước, định dạng, đường dẫn ảnh, thời gian tạo) vào cơ sở dữ liệu **Amazon DynamoDB**.

---

### Các điểm lưu ý sống còn khi triển khai

#### 1. Cạm bẫy "Vòng lặp vô tận" (Infinite Loop Trap)
> **Cảnh báo cực kỳ quan trọng:** Tuyệt đối không được cấu hình cho S3 bắn sự kiện vào Lambda, rồi bên trong Lambda lại ghi đè ảnh mới vào **cùng một bucket với cùng tiền tố (prefix)**. 
> Việc này sẽ tạo ra một vòng lặp chết người: Ảnh mới sinh ra lại kích hoạt Lambda chạy tiếp, và Lambda cứ gọi nhau hàng triệu lần trong vài phút, có thể đốt sạch hàng trăm USD tài khoản của bạn chỉ sau một đêm!
> Giải pháp: Luôn dùng 2 bucket tách biệt (`raw-images` và `processed-images`) hoặc chia folder tiền tố rõ ràng (`uploads/` và `thumbnails/`).

#### 2. Đoạn mã xử lý mẫu bằng Python

```python
import os
import urllib.parse
import boto3
from PIL import Image
import io
import time

s3_client = boto3.client('s3')
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table(os.environ['METADATA_TABLE'])
OUTPUT_BUCKET = os.environ['OUTPUT_BUCKET']

def lambda_handler(event, context):
    for record in event['Records']:
        source_bucket = record['s3']['bucket']['name']
        key = urllib.parse.unquote_plus(record['s3']['object']['key'])
        
        # 1. Đọc ảnh gốc từ S3 vào bộ nhớ RAM
        response = s3_client.get_object(Bucket=source_bucket, Key=key)
        image_bytes = response['Body'].read()
        
        # 2. Xử lý co giãn ảnh tỉ lệ chuẩn
        image = Image.open(io.BytesIO(image_bytes))
        image.thumbnail((300, 300))
        
        buffer = io.BytesIO()
        image.save(buffer, 'JPEG', quality=85)
        buffer.seek(0)
        
        # 3. Đẩy ảnh thu nhỏ sang bucket đích
        output_key = f"thumbnails/{key}"
        s3_client.put_object(
            Bucket=OUTPUT_BUCKET,
            Key=output_key,
            Body=buffer,
            ContentType='image/jpeg'
        )
        
        # 4. Ghi thông tin metadata vào DynamoDB
        table.put_item(
            Item={
                'image_id': key,
                'timestamp': int(time.time()),
                'source_bucket': source_bucket,
                'thumbnail_key': output_key,
                'width': image.width,
                'height': image.height
            }
        )
        
    return {'statusCode': 200, 'body': 'Xử lý ảnh thành công!'}
```

---

### Mẹo tối ưu hóa trong môi trường thực tế

* **Gắn Dead-Letter Queue (DLQ):**  
  Nên cấu hình một hàng đợi Amazon SQS làm DLQ cho Lambda. Khi có ai đó cố tình upload một file ảnh bị lỗi hoặc file rác khiến thư viện không mở được, Lambda thử lại vài lần thất bại sẽ đẩy thông tin lỗi vào SQS để chúng ta kiểm tra, tránh làm mất dấu vết.
* **Tăng tốc Lambda bằng cấu hình RAM:**  
  Trên AWS Lambda, khi bạn tăng mức RAM (ví dụ từ 256MB lên 1024MB), AWS sẽ cấp phát thêm năng lượng CPU tương ứng. Với các tác vụ nặng về tính toán hình ảnh như resize ảnh, thời gian chạy có thể giảm tới 4 lần, giúp tổng chi phí thực tế đôi khi lại rẻ hơn mức RAM thấp!
* **Mở rộng dung lượng đĩa đệm `/tmp`:**  
  Mặc định Lambda cấp 512MB bộ nhớ đệm `/tmp`. Nếu xử lý các file video ngắn hoặc ảnh chụp camera chất lượng cao vài trăm MB, bạn có thể tăng dung lượng ổ đĩa này lên tối đa 10GB.

---

### Lời kết
Mô hình Serverless Event-Driven không chỉ giúp hệ thống của bạn hoạt động bền bỉ, không sợ bị quá tải khi lượng người dùng tăng đột biến mà còn giúp tiết kiệm tối đa ngân sách vì bạn chỉ trả đúng từng mili-giây tài nguyên máy chủ thực sự thực hiện xử lý ảnh.
