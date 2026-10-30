---
title: "Week 10 Worklog"
date: 2025-10-13
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

# Week 10: Infrastructure as Code & Automated CI/CD Pipelines

### Week 10 Objectives:
* Adopt Infrastructure as Code (IaC) principles using AWS CloudFormation and Terraform.
* Build automated continuous integration and continuous deployment (CI/CD) pipelines using GitHub Actions.
* Secure pipeline secrets and automate unit testing, linting, and infrastructure provisioning.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Studied declarative Infrastructure as Code fundamentals: State management, drift detection, and idempotency.<br>- Authored a CloudFormation YAML template defining an S3 bucket with versioning, lifecycle rules, and bucket policy. | 13/10/2025 | 13/10/2025 | [AWS CloudFormation Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/) |
| **Tue** | - Practiced deploying CloudFormation stacks via AWS CLI (`aws cloudformation deploy`).<br>- Explored Terraform basics: Providers, Resources, Variables, Outputs, and remote state storage in Amazon S3 with DynamoDB state locking. | 14/10/2025 | 14/10/2025 | [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) |
| **Wed** | - Created a GitHub Actions workflow triggered on git push to the `main` branch.<br>- Configured OpenID Connect (OIDC) between GitHub Actions and AWS IAM, eliminating long-lived AWS secret keys in GitHub Secrets. | 15/10/2025 | 15/10/2025 | [GitHub OIDC with AWS](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services) |
| **Thu** | - Built a multi-step CI pipeline: Code checkout -> dependency installation -> unit tests -> code linter execution -> build artifact generation.<br>- Implemented automated static website deployment to S3 followed by CloudFront cache invalidation upon successful build. | 16/10/2025 | 16/10/2025 | [GitHub Actions Documentation](https://docs.github.com/en/actions) |
| **Fri** | - Added branch protection rules requiring status checks to pass before merging Pull Requests.<br>- Performed a simulated failure test in a staging branch to verify pipeline rollbacks.<br>- Documented CI/CD workflows and submitted weekly worklog. | 17/10/2025 | 17/10/2025 | [AWS DevOps Best Practices](https://aws.amazon.com/devops/) |

### Week 10 Achievements & Key Takeaways:
* **Elimination of ClickOps:** Transitioned completely from manual console clicking to reproducible, version-controlled code for provisioning cloud infrastructure.
* **Keyless Security with OIDC:** Replaced dangerous long-lived access keys in GitHub Secrets with dynamic, short-lived IAM credentials authenticated via OIDC.
* **Rapid Release Velocity:** Reduced code deployment time from 25 minutes of manual steps to an automated, reliable 2-minute pipeline triggered on every commit.
