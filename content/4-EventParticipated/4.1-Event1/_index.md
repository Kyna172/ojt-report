---
title: "Event 1"
date: 2025-08-11
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Summary Report: "GenAI-powered App & Database Modernization Workshop"

### Event Metadata
* **Event Name:** GenAI-powered App-DB Modernization Workshop
* **Date & Time:** August 13, 2025 | 09:00 – 17:00
* **Venue:** 26th Floor, Bitexco Financial Tower, District 1, Ho Chi Minh City
* **Role:** Attendee

---

### Keynote Speakers
* **Jignesh Shah** – Director, Open Source Databases at AWS
* **Erica Liu** – Senior GTM Specialist, App Modernization at AWS
* **Fabrianne Effendi** – Associate Specialist Solutions Architect, Serverless at AWS

---

### Executive Workshop Highlights

#### 1. Identifying the Bottlenecks of Legacy Monoliths
* **Delayed Time-to-Market:** Tightly coupled codebases turn minor feature deployments into high-risk release events, dragging release cycles from weeks to months.
* **Fragile Reliability:** A bug in a single non-critical module (e.g. reporting) can bring down the entire transactional application.
* **Operational Overhead:** Difficulty scaling specific components independently leads to excessive cloud resource over-provisioning.

#### 2. Domain-Driven Design (DDD) & Strategic Decomposition
* **Event Storming Methodology:** Mapping out real business processes chronologically through domain events before writing any code.
* **Bounded Contexts:** Defining clear, autonomous domain boundaries to isolate database ownership and API contracts.
* **Context Mapping:** Applying upstream/downstream integration patterns (Shared Kernel, Customer-Supplier, Anti-Corruption Layer).

#### 3. Event-Driven Asynchronous Architectures
* Transitioning from synchronous REST API cascades to loose coupling powered by message buses (Amazon EventBridge, Amazon SNS/SQS).
* Comparing communication models: Publish/Subscribe, Point-to-Point, and Event Streaming.

#### 4. Evolution of Serverless Compute
* Evaluating the compute spectrum: Virtual Machines (Amazon EC2) -> Containers (Amazon ECS/EKS) -> Serverless (AWS Fargate & AWS Lambda).
* How serverless eliminates operational undifferentiated heavy lifting, auto-scaling seamlessly with demand.

#### 5. Accelerating Transformations with Amazon Q Developer
* Leveraging Generative AI directly within the IDE for code explanation, test generation, and automated Java 8 to Java 17/21 runtime upgrades.
* Using AI-assisted agents to refactor monolithic stored procedures into lightweight cloud-native microservices.

---

### Personal Reflections & Student Takeaways

#### Business-First Architecture Mindset
The workshop completely shifted my perspective: Good software architecture is never about picking the trendiest framework; it is about accurately modeling the business domain and building systems that adapt swiftly to business changes.

#### Practical Application to My Capstone Project
* Applied loose coupling to my proposal: Rather than having the ingestion backend write directly to multiple destinations synchronously, I integrated asynchronous event messaging.
* Started adopting Amazon Q Developer in my daily development workflow, significantly accelerating debugging and documentation creation.

#### Networking Experience
Interacting directly with AWS Principal Architects during the networking break was inspiring. Seeing how enterprise architects break down massive million-user banking architectures gave me clear insights into what it takes to become a professional Cloud Solutions Architect.
