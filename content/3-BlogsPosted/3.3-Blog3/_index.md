---
title: "Blog 3"
date: 2025-08-11
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Building an Event-Driven Serverless Image Processing Pipeline with S3, Lambda & DynamoDB

### Problem Statement
In virtually every modern web platform (e-commerce, social media, blogging), users upload high-resolution profile pictures or product photos. If our application attempts to resize and process these large images synchronously inside the main web server process:
* Server threads get tied up waiting for heavy CPU-bound image transformations.
* User response times spike significantly, leading to poor user experience.
* Peak upload spikes can easily crash the web servers.

The elegant, cloud-native solution is to decouple ingestion from processing using an **asynchronous event-driven architecture**.

---

### Solution Architecture

```
[ User Uploads Image ]
          |
          v
[ Amazon S3 (Upload Bucket) ]
          | (s3:ObjectCreated:* Event)
          v
[ AWS Lambda (Resizer Function) ]
     |                       |
     | (Save Thumbnail)      | (Persist Metadata)
     v                       v
[ Amazon S3 (Resized) ]    [ Amazon DynamoDB ]
```

1. The frontend application uploads the original image directly to an **Amazon S3 Source Bucket** (optionally using S3 Presigned URLs).
2. Amazon S3 automatically fires an `ObjectCreated` event notification to an **AWS Lambda function**.
3. AWS Lambda streams the original image, performs proportional resizing and optimization (using the Pillow or Sharp image library), and writes the resized image to a **Target S3 Bucket**.
4. Simultaneously, Lambda saves the metadata record (original file size, thumbnail URL, timestamp, dimensions) into **Amazon DynamoDB**.

---

### Hands-on Implementation Details

#### 1. Preventing the Infinite Loop Trap
> **Critical Architectural Warning:** Never configure an S3 event notification to trigger a Lambda function that writes back into the **same bucket with the same prefix**. Doing so will cause an infinite execution loop where the output triggers another execution, rapidly draining your AWS budget.
> Always use two distinct buckets (e.g. `raw-images-bucket` and `processed-images-bucket`) or strict prefix filtering (`uploads/` vs `thumbnails/`).

#### 2. The Python Lambda Handler Code
Here is an idiomatic Python Lambda function using the `Pillow` library and AWS SDK (`boto3`):

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
        
        # Download image into memory buffer
        response = s3_client.get_object(Bucket=source_bucket, Key=key)
        image_bytes = response['Body'].read()
        
        # Process thumbnail
        image = Image.open(io.BytesIO(image_bytes))
        image.thumbnail((300, 300))
        
        buffer = io.BytesIO()
        image.save(buffer, 'JPEG', quality=85)
        buffer.seek(0)
        
        # Save thumbnail to output bucket
        output_key = f"thumbnails/{key}"
        s3_client.put_object(
            Bucket=OUTPUT_BUCKET,
            Key=output_key,
            Body=buffer,
            ContentType='image/jpeg'
        )
        
        # Record metadata in DynamoDB
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
        
    return {'statusCode': 200, 'body': 'Image processed successfully'}
```

---

### Resilience & Production Considerations

* **Dead-Letter Queues (DLQ):**  
  Attach an **Amazon SQS** Dead-Letter Queue to the Lambda function. If a corrupted image file fails processing after standard retries, the failed event payload is captured in SQS for debugging rather than lost silently.
* **Lambda Memory Configuration:**  
  Because AWS Lambda scales CPU power proportionally to allocated memory, assigning **1,024 MB or 1,536 MB** of RAM often makes image processing 3x faster, resulting in a *lower* net execution cost despite the higher per-second rate.
* **Ephemeral Storage (`/tmp`):**  
  For larger files (e.g., videos or massive raw camera formats), you can increase the `/tmp` scratch space up to 10 GB.

---

### Summary
By adopting an event-driven serverless architecture, you gain a resilient processing pipeline that scales automatically from 0 to 10,000 images per minute with zero maintenance overhead and virtually zero idle costs.
