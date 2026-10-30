---
title: "Blog 1"
date: 2025-08-11
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Least Privilege Security with Amazon EKS Pod Identity & Session Policies

### Introduction & Context
When running containerized workloads on Kubernetes with Amazon EKS, assigning AWS permissions to pods has always been a critical architectural decision. Historically, teams relied on **IAM Roles for Service Accounts (IRSA)**, which required setting up an OpenID Connect (OIDC) identity provider and complex trust policies per cluster.

AWS recently introduced **Amazon EKS Pod Identity**, streamlining role assumption down to an EKS add-on agent. Furthermore, the addition of **Session Policies** allows engineers to dynamically narrow IAM permissions for specific pods without needing to create new IAM roles for every microservice.

---

### Why Are Session Policies a Game-Changer?
In a multi-tenant or microservices Kubernetes cluster:
1. **The IAM Role Explosion Problem:** If Service A only needs read access to `bucket-a` and Service B only needs read access to `bucket-b`, engineers previously had to maintain two nearly identical IAM Roles.
2. **Quota Limitations:** AWS accounts enforce limits on the number of IAM Roles per account (default: 1,000 roles). High-density clusters quickly approach this limit.
3. **Session Policy Intersection:** With a Session Policy, the effective permissions are the **mathematical intersection** of the base IAM Role and the inline Session Policy:

$$\text{Effective Permissions} = \text{IAM Role Permissions} \cap \text{Session Policy Permissions}$$

> **Important Rule:** A session policy can only *restrict* or *narrow* permissions; it can never grant more access than the underlying IAM role permits.

---

### Architecture & How It Works

1. The Kubernetes Pod starts with an assigned ServiceAccount.
2. The Amazon EKS Pod Identity Agent DaemonSet intercepts AWS STS calls from the AWS SDK inside the container.
3. EKS requests temporary STS credentials from AWS IAM using the associated IAM Role and appends the configured **Session Policy**.
4. The pod receives credentials valid strictly for its specific scoped operations.

---

### Hands-on Configuration Example

#### 1. Define the Base IAM Role
The base IAM Role (`EKS-General-Storage-Role`) permits broad S3 read operations:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": "*"
    }
  ]
}
```

#### 2. Restrict per Pod via Session Policy
When creating the EKS Pod Identity Association via the AWS CLI, provide a Session Policy that restricts the pod to only read from `my-finance-reports-prod` bucket:

```bash
aws eks create-pod-identity-association \
  --cluster-name production-eks-cluster \
  --namespace finance-apps \
  --service-account finance-reporter \
  --role-arn arn:aws:iam::123456789012:role/EKS-General-Storage-Role \
  --client-token $(uuidgen)
```

The inline session policy applied to this association:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::my-finance-reports-prod/*"
    }
  ]
}
```

Even though the base role allows reading all S3 buckets, this specific pod cannot read from any bucket other than `my-finance-reports-prod`.

---

### Key Takeaways for DevOps Engineers
* **Clean Governance:** Manage a handful of generalized base roles while tailoring exact permissions per Kubernetes deployment.
* **Simplified Cluster Provisioning:** No need to configure an OIDC provider or manage complex IAM trust policies containing cluster OIDC issuer URLs.
* **Audit Trail:** AWS CloudTrail records show both the assumed role and the session name, ensuring complete traceability for security audits.
