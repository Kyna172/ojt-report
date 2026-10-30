---
title: "Week 3 Worklog"
date: 2025-08-25
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

# Week 3: Elastic Compute, Load Balancing & High Availability

### Week 3 Objectives:
* Gain comprehensive knowledge of Amazon EC2 instance families, purchase models, and storage volumes (EBS).
* Master Application Load Balancer (ALB) concepts including target groups and health checks.
* Implement Auto Scaling Groups (ASG) to achieve dynamic elasticity and high fault tolerance.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Analyzed EC2 instance families: General Purpose (t3, m5), Compute Optimized (c5), Memory Optimized (r5).<br>- Evaluated pricing models: On-Demand, Spot Instances, and Savings Plans.<br>- Wrote EC2 User Data bootstrap bash scripts to install Nginx and print server metadata automatically. | 25/08/2025 | 25/08/2025 | [EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/) |
| **Tue** | - Deep dive into Amazon Elastic Block Store (EBS) volume types: gp3, io2, st1.<br>- Practiced creating, attaching, partitioning, and formatting an extra gp3 EBS volume on Linux.<br>- Created snapshots of EBS volumes and tested restoring a volume from a snapshot. | 26/08/2025 | 26/08/2025 | [Amazon EBS Guide](https://docs.aws.amazon.com/ebs/) |
| **Wed** | - Created an Application Load Balancer (ALB) across multiple public subnets.<br>- Configured Target Groups and HTTP health check paths (`/health`).<br>- Registered two backend EC2 instances in different AZs and verified traffic round-robin distribution. | 27/08/2025 | 27/08/2025 | [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/) |
| **Thu** | - Created an Amazon Machine Image (AMI) from a configured web server instance.<br>- Defined an EC2 Launch Template with the custom AMI, security group, and IAM instance profile.<br>- Configured an Auto Scaling Group (ASG) with Min=2, Desired=2, Max=4 instances spanning two AZs. | 28/08/2025 | 28/08/2025 | [EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/) |
| **Fri** | - Conducted stress testing using the `stress` utility to simulate high CPU usage.<br>- Observed CloudWatch alarms triggering scale-out policy and terminating instances upon cooldown.<br>- Cleaned up ALB and ASG resources; summarized lessons learned. | 29/08/2025 | 29/08/2025 | [AWS Auto Scaling Policies](https://docs.aws.amazon.com/autoscaling/) |

### Week 3 Achievements & Key Takeaways:
* **True High Availability:** Built a complete self-healing, multi-AZ web cluster capable of surviving the complete loss of an Availability Zone.
* **Automation via User Data & Launch Templates:** Learned how to eliminate manual configuration when launching cloud instances.
* **Elastic Scalability:** Witnessed firsthand how cloud infrastructure dynamically scales up during traffic surges and scales in during idle periods, saving significant infrastructure costs.
