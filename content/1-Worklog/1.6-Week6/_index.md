---
title: "Week 6 Worklog"
date: 2025-09-15
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

# Week 6: Serverless Architecture (AWS Lambda & Amazon API Gateway)

### Week 6 Objectives:
* Master the event-driven serverless paradigm with AWS Lambda.
* Design and expose RESTful APIs using Amazon API Gateway.
* Build an end-to-end serverless CRUD microservice integrated with DynamoDB and automated error handling.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Studied AWS Lambda execution environments, memory allocation, execution timeouts, and cold starts.<br>- Wrote and deployed first Python Lambda functions handling standard JSON event payloads.<br>- Attached IAM execution roles granting least privilege access to AWS CloudWatch Logs. | 15/09/2025 | 15/09/2025 | [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/) |
| **Tue** | - Created an Amazon API Gateway REST API with resources (`/items`) and HTTP methods (`GET`, `POST`, `DELETE`).<br>- Configured Lambda Proxy Integration to pass query parameters, headers, and request bodies directly.<br>- Enabled Cross-Origin Resource Sharing (CORS) headers for frontend client interoperability. | 16/09/2025 | 16/09/2025 | [Amazon API Gateway Guide](https://docs.aws.amazon.com/apigateway/) |
| **Wed** | - Built a full serverless backend: API Gateway -> Lambda -> Amazon DynamoDB.<br>- Implemented structured CRUD endpoints: Create item, Fetch item by ID, List all items, Delete item.<br>- Added input data validation and customized standard HTTP status code responses (200, 400, 404, 500). | 17/09/2025 | 17/09/2025 | [Building Serverless APIs](https://aws.amazon.com/serverless/) |
| **Thu** | - Explored asynchronous Lambda event sources: Amazon S3 event notifications and DynamoDB Streams.<br>- Configured an S3 upload trigger to automatically resize user avatars upon upload via a Lambda function.<br>- Handled dead-letter queues (DLQ) using Amazon SQS for failed executions. | 18/09/2025 | 18/09/2025 | [Lambda Event Source Mapping](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html) |
| **Fri** | - Introduction to AWS Step Functions for orchestrating multi-step serverless workflows.<br>- Performed end-to-end API testing using Postman; reviewed Lambda cold start metrics.<br>- Documented API specs and submitted weekly worklog. | 19/09/2025 | 19/09/2025 | [AWS Step Functions](https://docs.aws.amazon.com/step-functions/) |

### Week 6 Achievements & Key Takeaways:
* **True Zero-Server Overhead:** Realized the massive productivity boost of serverless computing—no operating systems to patch, no servers to scale, zero payment when no requests arrive.
* **Stateless Microservices Design:** Learned to structure backend code cleanly into idempotent, stateless functions triggered by external events.
* **Cold Start Mitigation:** Understood techniques to minimize Lambda cold start latencies by keeping function packages lightweight and utilizing provisioned concurrency when necessary.
