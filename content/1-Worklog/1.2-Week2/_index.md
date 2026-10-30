---
title: "Week 2 Worklog"
date: 2025-08-18
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

# Week 2: Deep Dive into Amazon VPC & Hybrid Networking Concepts

### Week 2 Objectives:
* Master the architecture of Amazon Virtual Private Cloud (Amazon VPC).
* Design a custom VPC with multi-AZ high availability (Public & Private subnets).
* Configure Internet Gateway (IGW), NAT Gateway, Route Tables, and understand the difference between Security Groups and Network ACLs.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Studied IPv4 CIDR block calculations and subnetting best practices (`10.0.0.0/16`).<br>- Created a custom VPC named `Lab-VPC` spanning two Availability Zones (`ap-southeast-1a`, `ap-southeast-1b`). | 18/08/2025 | 18/08/2025 | [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/) |
| **Tue** | - Created 2 Public Subnets and 2 Private Subnets inside `Lab-VPC`.<br>- Attached an Internet Gateway (IGW) to allow internet ingress/egress for the public subnets.<br>- Built the Public Route Table with route destination `0.0.0.0/0` targeted to the IGW. | 19/08/2025 | 19/08/2025 | [VPC Routing Docs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html) |
| **Wed** | - Allocated an Elastic IP and provisioned a NAT Gateway in the Public Subnet.<br>- Configured the Private Route Table to route outbound traffic `0.0.0.0/0` through the NAT Gateway.<br>- Launched a test private EC2 instance to verify outbound internet access (e.g. running `yum update`). | 20/08/2025 | 20/08/2025 | [VPC NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) |
| **Thu** | - Analyzed security layers: Stateful Security Groups vs. Stateless Network ACLs (NACLs).<br>- Tested blocking specific IP addresses using NACL inbound deny rules.<br>- Learned about VPC Flow Logs and how to capture network traffic metadata. | 21/08/2025 | 21/08/2025 | [AWS Security Groups & NACLs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html) |
| **Fri** | - Introduction to VPC Peering and AWS Transit Gateway for multi-VPC topologies.<br>- Deleted NAT Gateway and released Elastic IP immediately after testing to prevent unexpected charges.<br>- Documented network architecture diagrams and submitted weekly worklog. | 22/08/2025 | 22/08/2025 | [VPC Peering Guide](https://docs.aws.amazon.com/vpc/latest/peering/) |

### Week 2 Achievements & Key Takeaways:
* **Networking Blueprint:** Gained complete clarity on how traffic flows from the internet through an IGW to public instances, and how private instances reach the outside world securely via a NAT Gateway.
* **Cost Sensitivity:** Realized that NAT Gateways incur hourly charges plus data processing fees, learning the engineering discipline of tearing down non-essential test infrastructure promptly.
* **Security Layering:** Learned to place databases and core backends strictly in Private Subnets with no direct public IP addresses.
