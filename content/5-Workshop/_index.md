---
title: "Workshop"
date: 2025-08-11
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Secure Hybrid Access to S3 using VPC Endpoints

#### Overview

**AWS PrivateLink** provides private connectivity to AWS services from Amazon VPCs and your on-premises networks without exposing your traffic to the Public Internet.

In this comprehensive hands-on workshop, you will learn how to design, configure, and validate VPC endpoints that allow hybrid cloud workloads to interact with AWS services with enterprise-grade isolation and zero internet egress dependencies.

You will implement and evaluate two distinct types of VPC endpoints for Amazon S3:
* **Gateway VPC Endpoint:** Directs traffic from subnets to Amazon S3 or DynamoDB via private AWS internal routing. Traffic is routed using VPC Route Table prefix lists at zero additional service cost.
* **Interface VPC Endpoint (powered by AWS PrivateLink):** Provisions elastic network interfaces (ENIs) with private IP addresses inside your VPC subnets, enabling seamless, secure access from on-premises datacenters over VPN or AWS Direct Connect.

---

#### Workshop Navigation

1. [Workshop Overview & Architecture](5.1-Workshop-overview/)
2. [Prerequisites & Base Stack Provisioning](5.2-Prerequiste/)
3. [Access S3 from Cloud VPC via Gateway Endpoint](5.3-S3-vpc/)
4. [Access S3 from On-Premises via Interface Endpoint](5.4-S3-onprem/)
5. [VPC Endpoint Policies & Data Perimeter (Bonus)](5.5-Policy/)
6. [Clean Up & Cost Avoidance](5.6-Cleanup/)
