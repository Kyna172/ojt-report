---
title: "Blog 1"
date: 2026-11-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# 5 Steps to Manage Amazon Bedrock Costs: Beyond Simply Reducing Token Usage

**This article was shared with the AWS Study Group community.**

**Published post:** [View the article on Facebook](https://www.facebook.com/share/p/19UsES7evm/)

## Article Content

When deploying Generative AI applications on AWS, costs are often evaluated based on token consumption and the pricing of individual models. However, as the number of users and processing requests increases, an important question arises: How can organizations identify where costs originate, determine who is consuming resources, and manage budgets effectively?

To address this challenge, an AWS Machine Learning Blog article presents a five-stage approach to managing Amazon Bedrock costs:

### 1. Attribute Costs

Identify which users, teams, or applications are responsible for resource consumption and associated costs. AWS Cost and Usage Report (CUR 2.0), IAM tags, and AWS Cost Explorer can help categorize and monitor costs across different workloads.

### 2. Monitor Usage

Use Model Invocation Logging to record model invocations. Logs can be delivered to Amazon CloudWatch Logs or Amazon S3, enabling analysis of token consumption and identification of applications with high resource usage.

### 3. Enforce Budget Controls

The AWS article describes three levels of cost control: using AWS Budgets to generate alerts when spending thresholds are exceeded, combining IAM with automation to restrict access, or implementing a gateway to reject requests when application-defined spending limits are reached.

### 4. Optimize Costs

Use Intelligent Prompt Routing to select suitable models for different tasks and Prompt Caching to reuse previously processed context, reducing the cost of repeated processing. Setting appropriate token limits can also help prevent unnecessary resource consumption.

### 5. Review and Improve

Regularly review indicators such as model usage, failed requests, and Prompt Caching effectiveness. These observations can guide adjustments to resource consumption and cost-management policies.

### Conclusion

These five stages form a continuous improvement cycle. Rather than focusing solely on billing reports, this approach helps organizations proactively monitor, control, and optimize Amazon Bedrock costs throughout application operations.

## Picture

<img width="1600" height="402" alt="image" src="https://github.com/user-attachments/assets/b96601b0-4014-402e-9a26-0095087698d6" />

## References

AWS Machine Learning Blog – *Managing Amazon Bedrock costs end to end: A playbook for FinOps and platform teams* (October 30, 2026).

[Read the original article on AWS](https://aws.amazon.com/vi/blogs/machine-learning/managing-amazon-bedrock-costs-end-to-end-a-playbook-for-finops-and-platform-teams/)
