---
title: "Week 7 Worklog"
date: 2025-09-22
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

# Week 7: Cloud Security, Identity & Governance

### Week 7 Objectives:
* Master the Principle of Least Privilege across AWS Identity and Access Management (IAM).
* Implement data encryption at rest and in transit using AWS Key Management Service (AWS KMS).
* Secure application credentials with AWS Secrets Manager and establish audit compliance via AWS CloudTrail.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Studied the evaluation logic of IAM policies: Explicit Deny > Explicit Allow > Default Deny.<br>- Authored fine-grained customer-managed policies with condition keys (`aws:PrincipalArn`, `aws:SourceIP`).<br>- Practiced assuming IAM Roles across services and understanding temporary credentials issued by AWS STS. | 22/09/2025 | 22/09/2025 | [IAM Policy Evaluation Logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html) |
| **Tue** | - Created symmetric Customer Managed Keys (CMK) in AWS KMS with dedicated key policies.<br>- Enabled automated annual key rotation and tested encrypting/decrypting sensitive strings via CLI.<br>- Integrated KMS encryption with Amazon S3 bucket default encryption and EBS volumes. | 23/09/2025 | 23/09/2025 | [AWS KMS Developer Guide](https://docs.aws.amazon.com/kms/) |
| **Wed** | - Stored database credentials and third-party API keys securely in AWS Secrets Manager.<br>- Enabled automated rotation schedules with an AWS-provided rotation Lambda function.<br>- Retrieved secrets programmatically in Python code, avoiding hardcoded secrets in source files. | 24/09/2025 | 24/09/2025 | [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/) |
| **Thu** | - Configured an AWS CloudTrail multi-region trail logging management and S3 data events.<br>- Created Amazon Athena tables to query CloudTrail JSON logs with SQL queries for forensic investigation.<br>- Configured Amazon SNS alerts when unauthorized API calls (e.g., `AccessDenied`) occur. | 25/09/2025 | 25/09/2025 | [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/) |
| **Fri** | - Deployed AWS WAF (Web Application Firewall) on an Application Load Balancer.<br>- Configured AWS Managed Rules against SQL Injection (SQLi) and Cross-Site Scripting (XSS).<br>- Summarized security architecture patterns and completed weekly worklog. | 26/09/2025 | 26/09/2025 | [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/) |

### Week 7 Achievements & Key Takeaways:
* **Zero Hardcoded Credentials:** Established the mandatory practice of storing all tokens, passwords, and connection strings exclusively in Secrets Manager or Parameter Store.
* **Auditability & Traceability:** Mastered CloudTrail log querying, allowing instant answers to "Who made what API call, from which IP, and at what timestamp?".
* **Defense in Depth:** Applied layered security across IAM identity controls, KMS cryptographic boundaries, and edge WAF inspection.
