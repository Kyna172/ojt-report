---
title: "First Cloud AI Journey: Weekly Meet Up 24/10"
date: 2026-10-24
weight: 1
chapter: false
pre: "<b> 4.4. </b>"
---

## Event Video: [Watch on YouTube](https://www.youtube.com/watch?v=dJiP5890kTg)

### Event Objectives

* Gain in-depth knowledge and practical insights into Cloud and AI Agent technologies from Tech Leads and enterprise engineers.
* Explore solutions for optimizing infrastructure architecture, information security, and cost management on AWS.
* Learn how to build and deploy AI Agent applications (Voice AI, Pentest Agent, Agent Framework) in production environments.
* Network and exchange experiences with the AWS Student Builder Group community and technology experts.

### List of Speakers

* **Kiet Tran** - Revve AI
* **Long Huynh** - Styl Solution
* **Thinh Nguyen** - Styl Solution
* **Xuan An** - Leader of AWS Student Builder Group HCMUTE
* **Khoa Kieu** - Tech Lead at ACB
* **Nghi Danh** - AWS Community Builder

### Key Highlights

#### Session 1: Hear, Think, Speak - Building a Vietnamese Voice-AI Contact Center on AWS

* **Voice AI Architecture**: Solutions for optimizing network transmission and processing to reduce call latency to approximately 1.8 seconds, enabling smoother and more natural voice interactions.
* **Live Demonstration**: Experienced an AI-powered system capable of automatically conducting preliminary interviews for the Cloud Engineer position entirely in Vietnamese, with flexible responses.

#### Session 2: AWS Resource Access Manager (RAM)

* **Secure Resource Sharing**: Methods for sharing resources between independent accounts within the same AWS Organization to optimize costs and support centralized network management.
* **Multi-Layer Access Management**: Combining IAM policies (permission granting) and Service Control Policies (SCPs) to establish permission boundaries and prevent privilege escalation.

#### Session 3: AWS Pentest with AWS Continuum / Security Agent

* **Early Infrastructure Security Assessment**: Integrating automated Infrastructure as Code (IaC) checks for Terraform directly into GitLab/GitHub pull request workflows to identify configuration vulnerabilities before merging.
* **Automated Pentesting with Security Agent**: Simulating a Security Agent acting as a real user to scan and perform automated penetration testing in SIT/UAT environments before production deployment.

#### Session 4: Amazon Bedrock AgentCore

* **Agent Runtime**: Optimizing operational costs by running MicroVMs on EC2 Spot infrastructure for Agent processing tasks.
* **Tiered Memory System**: A model that separates short-term memory (synchronous within a session) and long-term memory (asynchronous), helping Agents maintain detailed and accurate user context.

#### Session 5: Kiro Crew - AI Agent 24/7 Review Code & System Monitoring

* **Task Automation**: Building AI Agents that operate 24/7 to support code reviews and monitor system operational status.
* **Flexible Artifact Generation**: Enabling Agents to automatically collect real-world job data and visualize it as charts directly within the chat interface.
* **Context Window & Token Management**: The *Auto Compact* mechanism automatically compresses context when usage reaches 70–90% of capacity, combined with the *Break down context* feature to track token consumption across individual components.
* **Security & Memory Management**: Implementing Guardrails to prevent AI from independently executing dangerous commands (such as deleting infrastructure or exposing secrets and credentials), while cleaning up outdated memory to control costs.

### Key Learnings

#### Design Thinking & Architecture

* **Latency Management**: Practical lessons on balancing AI model accuracy and real-time response speed in Voice AI applications.
* **Shift-Left Security**: Introducing security checks (IaC reviews and automated penetration testing) early in CI/CD pipelines instead of waiting until systems reach production.
* **AI Agent Lifecycle Management**: Understanding the importance of managing memory, context windows, and resource costs (EC2 Spot and token consumption) when deploying Agents in production environments.

#### Infrastructure Engineering & Security

* **Privilege Boundaries**: Combining IAM policies and SCPs with AWS RAM to enforce the principle of least privilege at the enterprise level.
* **Generative AI Security**: Implementing Guardrails for AI Agents to control their behavior and prevent destructive infrastructure commands or sensitive data exposure.

### Practical Applications

* **Integrating Security Scans into CI/CD**: Exploring how to incorporate IaC security checks (Terraform reviews) into GitHub/GitLab pull request workflows for coursework or personal projects.
* **Applying Context & Memory Management**: Using context compression and tiered memory approaches when developing chatbots or integrating LLM APIs.
* **Practicing AWS Permission Management**: Experimenting with AWS Organizations, AWS RAM, and SCP configurations to gain a deeper understanding of cloud security architecture.
* **Networking & Continuous Learning**: Strengthening connections with experienced professionals, learning from their experiences, and contributing more actively to technology communities.

### Event Experience

The **First Cloud AI Journey Meet Up (October 24, 2026)**, held on the 26th floor of Bitexco Financial Tower, was a valuable learning experience that provided practical knowledge and insights from industry experts.

#### Learning from Speakers & Real-World Challenges

* I was particularly impressed by Revve AI's **Live Voice AI Interview Demo** and how the speakers addressed the challenge of achieving approximately 1.8-second latency.
* I gained practical insights into infrastructure management from Styl Solution, as well as experiences with AgentCore and Kiro Crew from HCMUTE and ACB.

#### Technical Experience & Personal Development

* I learned more about token management, preventing excessive costs when running AI Agents 24/7, and implementing security Guardrails.
* I recognized the gap between theoretical knowledge and real-world enterprise practices, which motivated me to continue networking, learning, and improving my technical skills throughout my cloud journey.

> Overall, the five sessions not only introduced advanced Cloud and AI Agent technologies but also provided motivation and helped me develop a clearer direction for my future technical career.

#### Event Photos

<img width="960" height="640" alt="Photo from the First Cloud AI Journey Weekly Meet Up" src="https://github.com/user-attachments/assets/9c65fb36-cd86-46c1-ac11-ae66b3d72590" />

<img width="960" height="640" alt="Activities during the First Cloud AI Journey Meet Up" src="https://github.com/user-attachments/assets/d871db56-543c-4f25-a6ca-9eefd52fba25" />

<img width="1280" height="960" alt="Photo documenting participation in the First Cloud AI Journey event" src="https://github.com/user-attachments/assets/388cbc25-83d5-4e0e-a220-391f3a8be7b1" />
