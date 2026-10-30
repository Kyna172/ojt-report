---
title: "Event 2"
date: 2025-08-11
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: "AWS Community Day Vietnam 2025"

### Event Metadata
* **Event Name:** AWS Community Day Vietnam 2025
* **Date & Time:** September 20, 2025 | 08:30 – 16:30
* **Venue:** Grand Palace Convention Center, Tan Binh District, Ho Chi Minh City
* **Role:** Technical Attendee & Community Volunteer Support

---

### Event Context & Scale
**AWS Community Day** is the premier annual community-led cloud conference organized by AWS User Groups in Vietnam. In 2025, the conference gathered over **600+ cloud engineers, solution architects, tech leaders, and student developers**, featuring multiple parallel breakout tracks on Generative AI, Cloud Security, DevOps, and Data Platforms.

---

### Key Technical Sessions Attended

#### 1. Keynote: Building Enterprise-Ready GenAI Applications with Amazon Bedrock
* **Speaker:** AWS Community Hero & Enterprise Solutions Architects.
* **Core Takeaways:**
  * Rather than training large language models from scratch, enterprises achieve 90% of their business value by orchestrating Foundation Models (Claude 3.5 Sonnet, Llama 3, Amazon Titan) through **Amazon Bedrock**.
  * Implementing **Retrieval-Augmented Generation (RAG)** using Amazon OpenSearch Serverless / pgvector on Amazon RDS PostgreSQL to ground AI responses with internal business facts.
  * Enforcing enterprise governance with **Guardrails for Amazon Bedrock** to automatically redact PII (personally identifiable information) and block harmful prompts.

#### 2. Deep Dive: Kubernetes Cost Optimization on Amazon EKS
* **Speaker:** Head of DevOps, Regional Tech Unicorn.
* **Core Takeaways:**
  * Moving from legacy Cluster Autoscaler to **Karpenter**, the open-source Kubernetes node autoscaler built by AWS.
  * Karpenter evaluates unschedulable pod requirements within milliseconds and provisions precisely-sized EC2 Spot instances, reducing cluster compute costs by over 45%.
  * Combining Graviton ARM-based EC2 instances (`c7g`, `m7g`) with Karpenter to maximize price-to-performance efficiency.

#### 3. Breakout Track: Zero-Trust Security Architecture on AWS
* **Speaker:** AWS Principal Security Consultant.
* **Core Takeaways:**
  * "Never trust, always verify": Shifting from perimeter-based firewalls to identity-centric authorization at every layer.
  * Utilizing AWS IAM Roles Anywhere, AWS PrivateLink, and Amazon GuardDuty with automated Lambda remediation handlers.

---

### Student Experience & Volunteer Engagement

#### Volunteering Experience
Alongside attending technical sessions, I had the privilege of supporting the FCAJ community booth, assisting with registration check-ins, guiding fellow students to technical track rooms, and sharing my internship learning experiences with university juniors curious about cloud computing.

#### Hands-on Community Demos
At the community exhibition floor, I engaged with live demonstration booths:
* Interacted with an automated edge computer vision setup classifying objects via AWS IoT Greengrass.
* Tested real-time AI agents running on Amazon Bedrock to answer technical questions based on AWS documentation.

#### Networking & Career Horizons
Meeting senior DevOps leads and AWS Community Heroes in person was an eye-opening milestone. They shared practical career advice on obtaining certifications with hands-on depth rather than rote memorization, emphasizing the value of open-source contributions and technical blogging.

---

### Conclusion
Attending AWS Community Day Vietnam 2025 was a thrilling, enriching experience that deepened my passion for cloud-native engineering and solidified my goal of becoming a well-rounded Cloud Solutions Architect.
