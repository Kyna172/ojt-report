---
title: "Blog 3"
date: 2026-11-10
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# WHY DOES AN API STILL NEED THROTTLING WHEN AWS WAF IS ALREADY ENABLED?

**This article was shared with the AWS Study Group community.**

**Published post:** [View the article on Facebook](https://www.facebook.com/share/p/197T9SMqNq/)

## Article Content

When an API receives a large volume of requests, AWS WAF alone may not be sufficient to control all traffic reaching the backend. AWS WAF and API Gateway Throttling serve different purposes: one filters suspicious traffic early, while the other controls request rates before backend execution.

The example architecture follows **Client → Amazon CloudFront (AWS WAF) → Amazon API Gateway → AWS Lambda**, with Amazon CloudWatch providing monitoring across the protection layers.

### Key Takeaways

- **AWS WAF Rate-based Rules:** Monitor request frequency by IP address or other configured aggregation criteria to limit unusual traffic before it reaches API Gateway.
- **Scope-down Statements:** Allow rate-based rules to target specific endpoints, such as `/api/search`, instead of the entire website.
- **API Gateway Throttling:** Uses Rate Limits and Burst Limits to control request traffic and reduce pressure on AWS Lambda.
- **HTTP 403 and 429:** AWS WAF returns HTTP 403 by default for blocked requests, while API Gateway may return HTTP 429 when throttling limits are exceeded.
- **Direct API Access:** If the default `execute-api` endpoint remains accessible, clients may bypass the WAF protection associated with CloudFront.
- **CloudWatch Monitoring:** Combines WAF logs, API Gateway metrics/access logs, and Lambda metrics to identify where requests are blocked or processed.

### Practical Applications

For public APIs, combining AWS WAF with API Gateway Throttling helps limit unusual traffic, manage backend workloads, and reduce the risk of disrupting legitimate users.

A recommended approach is to test WAF Rate-based Rules using the **Count** action before switching to **Block**. Direct access to API Gateway should also be reviewed, while logs and metrics are monitored to verify the effectiveness of each protection layer.

## Picture

<img width="2438" height="540" alt="image" src="https://github.com/user-attachments/assets/f93d7db8-2739-4e7d-92f4-d2ef2fe0d29b" />

## References

- [AWS Documentation – Rate-based Rule Settings in AWS WAF](https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-rate-based-high-level-settings.html)
- [AWS Documentation – API Gateway Request Throttling](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html)
