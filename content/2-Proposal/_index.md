---
title: "Proposal"
date: 2025-08-11
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# IoT Weather Platform for Lab Research
## A Unified AWS Serverless Solution for Real-Time Weather Monitoring

### 1. Executive Summary
The IoT Weather Platform is designed for the ITea Lab research team in Ho Chi Minh City to enhance microclimate weather data collection, visualization, and automated analytics. It supports up to 5 distributed weather stations with built-in scalability to 15 stations, utilizing Raspberry Pi edge nodes paired with ESP32 sensor modules to transmit telemetry over MQTT. 

The platform leverages modern AWS Serverless services to provide real-time dashboarding, predictive analytics, and cost-optimized operations, secured with role-based access for lab researchers via Amazon Cognito.

---

### 2. Problem Statement
#### The Current Challenge
Existing research weather stations depend heavily on manual, on-site data extraction using SD cards. As the number of deployed nodes increases, this process quickly becomes labor-intensive and prone to data gaps. Moreover, third-party commercial IoT platforms charge high recurring subscription fees while offering rigid, black-box architectures unsuitable for customized academic research.

#### The Proposed Solution
Our architecture implements an end-to-end cloud pipeline:
* **Ingestion:** **AWS IoT Core** ingests real-time MQTT sensor telemetry securely with X.509 device certificates.
* **Storage & Data Lake:** Raw JSON readings are batched directly into an **Amazon S3 Data Lake**.
* **ETL Transformation:** **AWS Glue Crawlers** catalog schemas, and scheduled **AWS Glue ETL** jobs transform raw records into optimized columnar Apache Parquet files stored in an analytics bucket.
* **Processing & API:** **AWS Lambda** and **Amazon API Gateway** expose lightweight REST APIs for device management and historical queries.
* **Frontend Application:** An interactive **Next.js** web dashboard hosted on **AWS Amplify** provides live visualization, interactive charting, and device telemetry metrics.
* **Authentication:** **Amazon Cognito** handles user authentication, ensuring restricted access to authorized research personnel.

#### Benefits & Return on Investment (ROI)
* **Automation:** Completely eliminates manual on-site data harvesting, saving dozens of research hours monthly.
* **Cost Efficiency:** Architecture costs only approximately **$0.70 USD/month** (~$8.40 USD/year) via AWS Free Tier and Serverless on-demand billing.
* **Extensibility:** Provides a solid, reusable dataset for future Machine Learning and AI climate forecasting models.

---

### 3. Solution Architecture

The serverless platform architecture is divided into the Edge Ingestion Layer and the Cloud Processing Platform:

![IoT Weather Station Edge Architecture](/images/2-Proposal/edge_architecture.jpeg)

![IoT Weather Platform Cloud Architecture](/images/2-Proposal/platform_architecture.jpeg)

#### Key AWS Services Used:
* **AWS IoT Core:** Handles mutual TLS authentication and message brokering for MQTT sensor payloads.
* **AWS Lambda:** Serverless compute for lightweight API backends and event-triggered processing.
* **Amazon API Gateway:** Exposes secure REST endpoints with request validation and throttling.
* **Amazon S3:** Highly durable storage for raw JSON telemetry and processed Parquet analytical datasets.
* **AWS Glue:** Serverless data cataloging and PySpark ETL transformations.
* **AWS Amplify:** Full-stack hosting for the responsive Next.js web console.
* **Amazon Cognito:** User directory and JWT authorization for lab members.

---

### 4. Technical Implementation Phases

1. **Phase 1: Architecture Design & Hardware Prototyping (Month 0 - Pre-internship)**  
   Researched ESP32 sensor pinouts, calibrated temperature/humidity/pressure sensors, and designed the AWS target architecture.
2. **Phase 2: Cost Modeling & Feasibility Validation (Month 1)**  
   Modeled exact request quotas and data throughput using the AWS Pricing Calculator to confirm monthly costs stay below $1 USD.
3. **Phase 3: Core Service Provisioning & Pipeline Integration (Month 2)**  
   Configured IoT Core rules, S3 storage buckets, Glue ETL scripts, and Lambda REST API endpoints using AWS CDK/CloudFormation.
4. **Phase 4: Dashboard Deployment, Field Testing & Optimization (Month 3)**  
   Built the Next.js frontend, deployed on Amplify, completed end-to-end load testing, and calibrated edge Wi-Fi reconnection handling.

---

### 5. Timeline & Milestones
* **Milestone 1:** Edge firmware stabilized, sensor telemetry flowing reliably to AWS IoT Core.
* **Milestone 2:** S3 Data Lake and automated Glue ETL pipeline operational.
* **Milestone 3:** Amplify web dashboard connected with Cognito authentication and live charts.
* **Milestone 4:** Full stress testing and final documentation completed.

---

### 6. Budget Estimation

Estimated monthly cost breakdown using the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01):

| Service | Monthly Volume / Usage | Estimated Monthly Cost |
| :--- | :--- | :--- |
| **AWS IoT Core** | 5 stations, ~45,000 MQTT messages/month | $0.08 USD |
| **Amazon S3** | 6 GB storage, ~2,100 PUT/GET requests | $0.15 USD |
| **AWS Lambda** | 1,000 invocations, 512 MB memory | $0.00 USD (Free Tier) |
| **Amazon API Gateway** | 2,000 REST requests | $0.01 USD |
| **AWS Glue** | 1 Crawler + 2 DPU-hours ETL batching | $0.09 USD |
| **AWS Amplify** | Static hosting & Next.js SSR build/bandwidth | $0.35 USD |
| **Data Transfer Out** | 1 GB egress bandwidth | $0.02 USD |
| **Total Cloud Cost** | **Estimated Total** | **~$0.70 USD / month** |

*Hardware investment:* Existing lab equipment (ESP32, sensors, Raspberry Pi 5) valued at ~$265 USD was repurposed, incurring zero additional hardware expense.

---

### 7. Risk Assessment & Mitigation

* **Intermittent Network Disconnectivity:**  
  *Risk:* Edge stations may drop Wi-Fi connection during stormy weather.  
  *Mitigation:* Edge Raspberry Pi stores readings in a local SQLite buffer with Docker; cached payloads automatically sync to AWS IoT Core once network connectivity is restored.
* **Sensor Drift & Hardware Failures:**  
  *Risk:* Sensor corrosion or incorrect calibration values.  
  *Mitigation:* Sensor health heartbeat telemetry and spare sensor kits ready for immediate hot-swapping.
* **Unexpected Cloud Billing Spikes:**  
  *Risk:* Errant infinite loops or retry storms driving up serverless charges.  
  *Mitigation:* AWS Budgets with $2/month threshold alerts and hard concurrency limits set on Lambda functions.

---

### 8. Expected Outcomes & Project Impact
* **Autonomous Operations:** Continuous 24/7 climate monitoring without human intervention.
* **Empirical Research Asset:** High-fidelity, clean historical weather dataset ready for machine learning model training and academic publication.
