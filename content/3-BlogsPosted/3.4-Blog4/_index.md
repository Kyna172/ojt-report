---
title: "Blog 4"
date: 2026-11-10
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

# AMAZON BEDROCK: CONTROLLING REQUESTS AND TOKEN USAGE BEFORE COSTS INCREASE

**This article was shared with the AWS Study Group community.**

**Published post:** [View the article on Facebook](https://www.facebook.com/share/p/1cJCsM4u1G/)

## Article Content

When deploying Generative AI applications with Amazon Bedrock, limiting the number of API requests alone is not sufficient for effective cost management. Even valid requests can consume large numbers of tokens due to long prompts or extensive outputs, especially in multi-tenant applications.

To reduce unexpected expenses, a layered architecture can combine **Amazon CloudFront, AWS WAF, API Gateway, AWS Lambda, DynamoDB, and Amazon Bedrock**, supported by monitoring and usage analytics services.

### Key Takeaways

- **AWS WAF and Amazon CloudFront:** Filter unusual traffic at the edge using Rate-based Rules, reducing unnecessary requests before they reach the application.
- **Amazon API Gateway:** Provides authentication, authorization, and throttling through Rate Limits and Burst Limits to control incoming traffic.
- **AWS Lambda and Amazon DynamoDB:** Implement a Quota Controller to enforce per-tenant request or token limits before invoking Bedrock.
- **Atomic and Conditional Updates:** Help maintain accurate quota records when multiple requests are processed concurrently.
- **Token Usage Tracking:** Estimates token consumption before inference and reconciles it with actual usage after Bedrock returns a response.
- **Amazon CloudWatch and SNS:** Monitor model invocations, input/output tokens, and send notifications when usage exceeds configured thresholds.
- **Amazon S3 and Athena:** Store and analyze usage data by tenant, model, or time period to support more detailed cost management.

### Practical Applications

This architecture is useful for AI applications serving multiple users or tenants, where individual usage limits are needed to reduce unexpected costs caused by repeated requests or excessive token consumption.

For smaller applications, **Lambda, DynamoDB, and CloudWatch** can provide a practical starting point. S3 and Athena can be introduced later when more advanced usage analysis is required.

Application-level quotas must also account for concurrent requests, retries, and differences between estimated and actual token usage. These controls help reduce unexpected consumption but do not guarantee an absolute spending limit.

## Picture

<img width="3754" height="540" alt="image" src="https://github.com/user-attachments/assets/4443cc50-51a8-4a68-9bb1-5f95ce803e21" />

## References

- [AWS Documentation – Amazon Bedrock Quotas](https://docs.aws.amazon.com/bedrock/latest/userguide/quotas.html)
- [AWS Documentation – Model Invocation Logging](https://docs.aws.amazon.com/bedrock/latest/userguide/model-invocation-logging.html)
