---
title: "Week 8 Worklog"
date: 2025-09-29
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

# Week 8: Monitoring, Observability & Logging (Amazon CloudWatch)

### Week 8 Objectives:
* Master observability pillars (Metrics, Logs, Traces) on AWS using Amazon CloudWatch and AWS X-Ray.
* Create automated Metric Alarms integrated with Amazon SNS for real-time incident alerting.
* Query structured application logs efficiently with CloudWatch Logs Insights.

### Tasks Carried Out This Week:
| Day | Tasks | Start Date | Completion Date | Reference Materials |
| :--- | :--- | :--- | :--- | :--- |
| **Mon** | - Studied Amazon CloudWatch fundamentals: Standard metrics, custom metrics, and metric dimensions.<br>- Installed and configured the CloudWatch Unified Agent on Linux EC2 instances to collect memory and disk utilization. | 29/09/2025 | 29/09/2025 | [CloudWatch Agent Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html) |
| **Tue** | - Designed a centralized CloudWatch Dashboard displaying CPU utilization, memory pressure, HTTP 4xx/5xx error rates, and disk I/O.<br>- Configured custom refresh intervals and organized widgets for quick incident triage. | 30/09/2025 | 30/09/2025 | [CloudWatch Dashboards](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html) |
| **Wed** | - Created CloudWatch Alarms monitoring CPU utilization > 80% for 2 consecutive evaluation periods (5 minutes).<br>- Integrated alarm state changes (`OK`, `ALARM`, `INSUFFICIENT_DATA`) with Amazon Simple Notification Service (SNS).<br>- Tested alert dispatch to personal email and a Slack incoming webhook. | 01/10/2025 | 01/10/2025 | [Using CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| **Thu** | - Set up CloudWatch Log Groups with retention policies to prevent unbounded storage costs.<br>- Practiced writing queries in CloudWatch Logs Insights to parse JSON logs, filter error stacks, and calculate request percentiles (`p95`, `p99`). | 02/10/2025 | 02/10/2025 | [CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) |
| **Fri** | - Enabled AWS X-Ray active tracing on API Gateway and Lambda functions.<br>- Analyzed service maps to pinpoint downstream database bottlenecks and slow outbound HTTP calls.<br>- Submitted weekly worklog and documentation. | 03/10/2025 | 03/10/2025 | [AWS X-Ray Developer Guide](https://docs.aws.amazon.com/xray/) |

### Week 8 Achievements & Key Takeaways:
* **Proactive Rather Than Reactive:** Shifted mindset from waiting for users to complain about outages to receiving automated alerts the second metrics deviate from healthy baselines.
* **Rapid Root-Cause Analysis:** Learned to isolate the exact line number of an exception across millions of log lines within seconds using Logs Insights syntax.
* **End-to-End Tracing:** Visualized distributed microservice execution times with AWS X-Ray, identifying slow database queries effortlessly.
