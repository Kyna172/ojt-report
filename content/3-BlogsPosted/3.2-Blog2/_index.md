---
title: "Blog 2"
date: 2025-08-11
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# High-Performance & Secure Static Web Hosting with S3 & CloudFront OAC

### The Dilemma: Fast, Cheap, but Is It Secure?
Hosting single-page applications (React, Vue, Hugo, Next.js static exports) on **Amazon S3** is a beloved design pattern due to its near-infinite scalability, 99.999999999% (11 9's) data durability, and virtually negligible costs.

However, many beginner guides suggest checking **"Static Website Hosting"** on the S3 bucket and adding a public `s3:GetObject` bucket policy. 
This approach comes with severe downsides:
* The S3 bucket URL is completely public and vulnerable to scrapers, DDoS, and hotlinking.
* AWS S3 direct endpoints do not natively support modern HTTPS certificates on custom domain names.
* Data Transfer Out (DTO) directly from S3 is more expensive than routing through the global Content Delivery Network (CDN).

---

### The Modern Standard: CloudFront with Origin Access Control (OAC)
In 2022, AWS released **Origin Access Control (OAC)** to replace the legacy Origin Access Identity (OAI). OAC brings major improvements:
* Supports all S3 regions, including newly added ones.
* Supports Server-Side Encryption with AWS KMS (SSE-KMS).
* Supports dynamic HTTP `PUT`, `DELETE` methods if needed, alongside standard `GET` requests.

```
[ User Browser ]
       | (HTTPS / HTTP3 - Worldwide Edge Locations)
       v
[ Amazon CloudFront CDN ]
       | (Signed AWS SigV4 Request via OAC)
       v
[ Private Amazon S3 Bucket ] (Block All Public Access: ON)
```

---

### Implementation Guide

#### 1. Keep S3 Completely Private
Turn on **"Block all public access"** on your S3 bucket. Do not enable "Static website hosting". Keep it as a standard private storage bucket.

#### 2. Create the CloudFront Distribution
* Set the **Origin domain** to your S3 bucket's regional endpoint: `your-bucket-name.s3.ap-southeast-1.amazonaws.com`.
* Under **Origin access**, select **Origin access control settings (recommended)** and click **Create new OAC**.
* Select **Redirect HTTP to HTTPS** in the default cache behavior.
* Set default root object to `index.html`.

#### 3. Attach the S3 Bucket Policy
CloudFront generates a tailored bucket policy. Apply this policy to your S3 bucket:

```json
{
  "Version": "2012-10-17",
  "Statement": {
    "Sid": "AllowCloudFrontServicePrincipalReadOnly",
    "Effect": "Allow",
    "Principal": {
      "Service": "cloudfront.amazonaws.com"
    },
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::your-bucket-name/*",
    "Condition": {
      "StringEquals": {
        "AWS:SourceArn": "arn:aws:cloudfront::123456789012:distribution/EDFDVBD6EXAMPLE"
      }
    }
  }
}
```

Notice the crucial `AWS:SourceArn` condition key: It guarantees that **only your specific CloudFront distribution** can read objects from your bucket, preventing unauthorized distributions in other accounts from accessing your assets.

---

### Performance & Cost Optimization Tips

1. **Leverage Cache-Control Headers:**  
   Configure your build pipeline to upload static assets (like `.js` and `.css` files with content hashes) with long cache lifetimes:
   ```bash
   aws s3 cp ./build/static s3://your-bucket-name/static \
     --cache-control "public, max-age=31536000, immutable"
   ```
2. **Handle Single Page App Client-Side Routing:**  
   Add a custom error response in CloudFront: Map HTTP 403 / 404 error codes to respond with `/index.html` and HTTP status 200, allowing React Router to handle page routes smoothly.
3. **Invalidate Only What Changed:**  
   Avoid paying for excessive `/*` invalidations on busy repositories. Whenever possible, invalidate specific file paths (e.g., `/index.html`).

---

### Conclusion
By combining Amazon S3 with CloudFront and Origin Access Control, you get an enterprise-grade web hosting setup that is blazing fast, strictly secured, and costs merely pennies per month.
