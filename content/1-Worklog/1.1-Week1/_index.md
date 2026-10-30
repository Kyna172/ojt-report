---
title: "Week 1 Worklog"
date: 2025-08-11
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

# Week 1: Onboarding, AWS Fundamentals & CLI Setup

### Week 1 Objectives:
* Complete onboarding procedures, meet mentors and teammates in the First Cloud AI Journey program.
* Understand the core concepts of AWS Cloud infrastructure (Regions, Availability Zones, Edge Locations).
* Set up a dedicated AWS Free Tier development account and master basic CLI configuration.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Attended kickoff meeting, introduced myself to mentors and teammates.<br>- Reviewed internship rules, code of conduct, and evaluation criteria. | 11/08/2025 | 11/08/2025 | Intern Onboarding Guide |
| **Tue** | - Studied AWS Global Infrastructure: Regions, AZs, Local Zones, and Edge Locations.<br>- Explored the AWS Management Console navigation and service directory. | 12/08/2025 | 12/08/2025 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wed** | - Created AWS Free Tier account, set up Root account MFA and billing budget alerts.<br>- Initialized the first IAM Administrator user and configured IAM password policy. | 13/08/2025 | 13/08/2025 | [AWS IAM Documentation](https://docs.aws.amazon.com/iam/) |
| **Thu** | - Installed AWS CLI v2 on local machine.<br>- Configured AWS credentials (`aws configure`) with default region `ap-southeast-1` (Singapore).<br>- Tested basic commands (`aws sts get-caller-identity`, `aws ec2 describe-regions`). | 14/08/2025 | 14/08/2025 | [AWS CLI Reference](https://docs.aws.amazon.com/cli/) |
| **Fri** | - Practiced launching first EC2 instance (Amazon Linux 2023) via both AWS Console and CLI.<br>- Created SSH Key Pair, attached security group, and connected via SSH terminal.<br>- Wrote weekly summary and submitted weekly worklog to mentor. | 15/08/2025 | 15/08/2025 | [AWS EC2 User Guide](https://docs.aws.amazon.com/ec2/) |

### Week 1 Achievements & Key Takeaways:
* **Account Security Best Practice:** Understood the importance of locking away the Root account credentials and enforcing Multi-Factor Authentication (MFA) immediately.
* **Command Line Proficiency:** Got comfortable with running AWS CLI commands, understanding default profiles, and parsing JSON output.
* **Hands-on Confidence:** Successfully connected to a cloud compute instance from the local terminal using SSH, verifying that security groups act as stateful firewalls.
