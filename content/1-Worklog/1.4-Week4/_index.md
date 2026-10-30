---
title: "Week 4 Worklog"
date: 2025-09-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

# Week 4: Object Storage & Content Delivery Network (Amazon S3 & CloudFront)

### Week 4 Objectives:
* Master Amazon Simple Storage Service (Amazon S3) storage classes, bucket policies, and lifecycle management.
* Host a single-page application (SPA) securely on Amazon S3.
* Accelerate global content delivery and enforce HTTPS using Amazon CloudFront with Origin Access Control (OAC).

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Studied Amazon S3 storage tiers: Standard, Intelligent-Tiering, Standard-IA, One Zone-IA, Glacier Flexible, and Glacier Deep Archive.<br>- Created S3 buckets and practiced versioning, server-side encryption (SSE-S3 & SSE-KMS). | 01/09/2025 | 01/09/2025 | [Amazon S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/) |
| **Tue** | - Defined S3 Lifecycle Rules to transition older objects to Glacier after 30 days and expire incomplete multipart uploads.<br>- Configured S3 Object Lock and Cross-Region Replication (CRR) concepts. | 02/09/2025 | 02/09/2025 | [S3 Lifecycle Management](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html) |
| **Wed** | - Deployed a static HTML/React portfolio website onto an S3 bucket.<br>- Explored S3 Static Website Hosting vs. private bucket architectures.<br>- Analyzed security considerations regarding public read bucket policies. | 03/09/2025 | 03/09/2025 | [Hosting Static Websites on S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) |
| **Thu** | - Provisioned an Amazon CloudFront distribution pointing to the private S3 bucket origin.<br>- Configured Origin Access Control (OAC) to restrict bucket access exclusively to CloudFront.<br>- Enabled HTTPS redirection, gzip/brotli compression, and custom cache TTL policies. | 04/09/2025 | 04/09/2025 | [CloudFront OAC Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html) |
| **Fri** | - Tested cache invalidation (`/*`) when updating website assets.<br>- Measured response latency before and after CloudFront edge caching using curl/devtools.<br>- Summarized findings and submitted weekly worklog. | 05/09/2025 | 05/09/2025 | [CloudFront Caching](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Expiration.html) |

### Week 4 Achievements & Key Takeaways:
* **Storage Cost Optimization:** Mastered S3 Lifecycle policies, understanding how automated archiving can slash cloud storage expenses by up to 90% for cold data.
* **Security Through OAC:** Eliminated the common anti-pattern of opening S3 buckets publicly, adopting modern Origin Access Control (OAC) so users can only reach content via CloudFront edge caches.
* **Global Latency Reduction:** Observed instant page loading worldwide due to edge location caching, SSL termination, and HTTP/2 and HTTP/3 support.
