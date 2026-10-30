---
title: "Week 11 Worklog"
date: 2025-10-20
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

# Week 11: Workshop Development & Hands-on Lab Verification

### Week 11 Objectives:
* Design and structure a production-grade technical workshop: "Secure Hybrid Access to S3 using VPC Endpoints".
* Provision simulated hybrid environments using AWS CloudFormation, Transit Gateway, and strongSwan VPN.
* Author clear, reproducible step-by-step documentation in bilingual markdown format (English & Vietnamese).

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Defined the workshop architecture scope: Connecting on-premises networks and AWS VPCs to Amazon S3 privately without internet egress.<br>- Deployed the base CloudFormation stacks provisioning the Cloud VPC, simulated On-Premises VPC, and Site-to-Site VPN tunnels. | 20/10/2025 | 20/10/2025 | [AWS PrivateLink Docs](https://docs.aws.amazon.com/vpc/latest/privatelink/) |
| **Tue** | - Created a Gateway VPC Endpoint for S3; verified routing prefix list entries in the VPC Route Table.<br>- Tested accessing S3 buckets from an EC2 instance in a private subnet with no Internet Gateway.<br>- Captured screenshots, CLI outputs, and documented troubleshooting notes for Lab Part 1. | 21/10/2025 | 21/10/2025 | [Gateway VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html) |
| **Wed** | - Created an Interface VPC Endpoint (AWS PrivateLink) with elastic network interfaces (ENIs) inside private subnets.<br>- Verified private IP allocations and DNS names generated for the interface endpoint.<br>- Simulated on-premises requests via AWS Systems Manager Session Manager. | 22/10/2025 | 22/10/2025 | [Interface VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html) |
| **Thu** | - Configured Amazon Route 53 Private Hosted Zones and inbound resolver endpoints to simulate on-premises split-horizon DNS.<br>- Tested DNS resolution with `dig` and `nslookup` commands from the simulated on-premise EC2 instance.<br>- Implemented VPC Endpoint Bucket Policies to enforce least privilege access restrictions. | 23/10/2025 | 23/10/2025 | [Route 53 Resolver](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html) |
| **Fri** | - Conducted a complete end-to-end dry run following only the written lab guide to uncover any missing steps.<br>- Tested the teardown scripts to guarantee clean resource deletion with zero leftover charges.<br>- Formatted markdown files with callout notices, code blocks, and submitted weekly worklog. | 24/10/2025 | 24/10/2025 | Workshop Guidelines |

### Week 11 Achievements & Key Takeaways:
* **Deep Mastery of VPC Endpoints:** Grasped the architectural and cost differences between free Gateway Endpoints (VPC-internal only) and Interface Endpoints powered by PrivateLink (accessible across VPN/Direct Connect).
* **Technical Writing Excellence:** Realized that creating high-quality documentation requires putting oneself in the reader's shoes, verifying every single CLI flag, and testing edge cases.
* **Deterministic Lab Cleanup:** Formulated strict teardown procedures to ensure lab participants incur no recurring background fees after completing the tutorial.
