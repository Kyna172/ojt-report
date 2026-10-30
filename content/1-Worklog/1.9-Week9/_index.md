---
title: "Week 9 Worklog"
date: 2025-10-06
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

# Week 9: Containerization on AWS (Docker, Amazon ECR & Amazon ECS)

### Week 9 Objectives:
* Master application containerization using multi-stage Docker builds.
* Store, scan, and manage container images securely in Amazon Elastic Container Registry (ECR).
* Deploy and run serverless containerized services using Amazon Elastic Container Service (ECS) powered by AWS Fargate.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Studied Docker fundamentals, image layers, and best practices for writing lightweight Dockerfiles.<br>- Wrote a multi-stage Dockerfile for a Node.js/Go web application, reducing final image size from 850MB to 65MB. | 06/10/2025 | 06/10/2025 | [Docker Documentation](https://docs.docker.com/) |
| **Tue** | - Created a private container registry using Amazon ECR with immutable image tags.<br>- Configured ECR image vulnerability scanning on push to detect known CVEs automatically.<br>- Authenticated local Docker client via `aws ecr get-login-password` and pushed container images. | 07/10/2025 | 07/10/2025 | [Amazon ECR User Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/) |
| **Wed** | - Designed Amazon ECS architecture components: Clusters, Task Definitions, and Services.<br>- Authored an ECS Task Definition defining CPU/memory limits, environment variables from SSM Parameter Store, and container port mappings. | 08/10/2025 | 08/10/2025 | [Amazon ECS Developer Guide](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/) |
| **Thu** | - Provisioned an ECS Fargate Service running across private subnets behind an Application Load Balancer.<br>- Configured AWS Fargate serverless compute launch type, removing the need to manage EC2 host nodes.<br>- Verified seamless target group health checks and rolling zero-downtime updates. | 09/10/2025 | 09/10/2025 | [AWS Fargate Guide](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html) |
| **Fri** | - Tested ECS Service Auto Scaling based on incoming ALB Request Count Per Target.<br>- Reviewed vulnerability scanning findings in ECR and patched base images.<br>- Cleaned up ECS tasks and load balancers; submitted weekly worklog. | 10/10/2025 | 10/10/2025 | [ECS Service Auto Scaling](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-auto-scaling.html) |

### Week 9 Achievements & Key Takeaways:
* **The Power of Multi-Stage Builds:** Reduced container attack surface and image size drastically by excluding build-time tools from runtime artifacts.
* **Serverless Containerization:** Experienced the simplicity of AWS Fargate—just specify CPU and RAM, and AWS manages the underlying container execution fleet with zero node maintenance.
* **Zero-Downtime Deployments:** Understood how ECS coordinates with ALB to spin up new container tasks, wait for healthy checks, and drain old tasks without dropping a single active HTTP request.
