---
title: "Week 5 Worklog"
date: 2025-09-08
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

# Week 5: Relational & NoSQL Database Services (Amazon RDS & DynamoDB)

### Week 5 Objectives:
* Understand managed database architectures with Amazon Relational Database Service (Amazon RDS).
* Provision an RDS PostgreSQL instance with Multi-AZ failover and Read Replica scaling.
* Master Amazon DynamoDB core concepts: Partition Keys, Sort Keys, Global Secondary Indexes (GSIs), and serverless NoSQL performance.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Analyzed managed database benefits over self-hosted databases on EC2.<br>- Created a DB Subnet Group spanning two private subnets in `Lab-VPC`.<br>- Provisioned an Amazon RDS PostgreSQL db.t3.micro instance in Multi-AZ deployment. | 08/09/2025 | 08/09/2025 | [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) |
| **Tue** | - Connected to the RDS instance securely from a bastion host / EC2 private app server.<br>- Configured automated backup retention and created manual DB snapshots.<br>- Tested simulated Multi-AZ failover to examine failover duration and DNS switch behavior. | 09/09/2025 | 09/09/2025 | [RDS Multi-AZ Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html) |
| **Wed** | - Created a Read Replica in the same region to offload read-heavy query traffic from the primary instance.<br>- Practiced modifying DB parameter groups and enabling performance insights. | 10/09/2025 | 10/09/2025 | [RDS Read Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html) |
| **Thu** | - Introduction to NoSQL principles and Amazon DynamoDB serverless architecture.<br>- Created a DynamoDB table with Partition Key (`userId`) and Sort Key (`timestamp`).<br>- Experimented with On-Demand vs. Provisioned capacity modes, WCU/RCU calculations. | 11/09/2025 | 11/09/2025 | [Amazon DynamoDB Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) |
| **Fri** | - Created a Global Secondary Index (GSI) to query items by secondary attributes efficiently.<br>- Ran Python AWS SDK (boto3) scripts to perform `PutItem`, `GetItem`, and `Query` operations.<br>- Cleaned up RDS instances (taking final snapshots) and submitted weekly worklog. | 12/09/2025 | 12/09/2025 | [DynamoDB GSI Docs](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GSI.html) |

### Week 5 Achievements & Key Takeaways:
* **High Availability for Data:** Saw RDS Multi-AZ synchronously replicate transactions to a standby instance and failover automatically without data loss.
* **Read Scalability:** Learned how Read Replicas relieve pressure on primary relational databases for analytics and read-intensive applications.
* **NoSQL Query Mindset:** Understood that DynamoDB requires designing schemas based on access patterns rather than relational table normalization.
