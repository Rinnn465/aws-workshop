---
title: "Proposal"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Intelligent Scheduling Chatbot on AWS

**Date:** December 03, 2025  
**Team:** Vinhomies – FPT University

---

## Table of Contents

1. [Background and Motivation](#1-background-and-motivation)
2. [Solution Architecture](#2-solution-architecture)
3. [Activities and Deliverables](#3-activities-and-deliverables)
4. [Expected AWS Cost Breakdown](#4-expected-aws-cost-breakdown)
5. [Team](#5-team)
6. [Resources & Cost Estimates](#6-resources--cost-estimates)
7. [Acceptance](#7-acceptance)

## 1. BACKGROUND AND MOTIVATION

### 1.1 Executive Summary
The Intelligent Scheduling Chatbot on AWS is a fully serverless solution designed to automate appointment booking and customer support through Facebook Messenger.

The system integrates Large Language Models (LLMs) on Amazon Bedrock (Claude 3.5 Sonnet, Claude 3 Haiku, Claude 3 Sonnet) using a Text-to-SQL mechanism to query/execute SQL on a PostgreSQL database for complex scheduling operations and produce accurate, context-aware responses.


**Core Components:**
* **Frontend Layer:** Facebook Messenger integration via Webhook receiver.
* **Processing Layer:** Lambda functions for ChatHandler, Text2SQL Handler, Data Indexer.
* **Data Layer:** PostgreSQL (RDS) for appointment data; DynamoDB for cache/session.
* **AI Layer:** Amazon Bedrock with Claude 3.5 Sonnet (Text2SQL) & Claude 3 Haiku/Sonnet (ChatHandler).
* **Admin Dashboard / Consultant Portal:** React app hosted on S3 + CloudFront with Cognito Authentication.

The entire system is deployed on AWS Serverless architecture in the Asia Pacific (Tokyo) region, ensuring scalability, cost efficiency, and operational reliability.

### 1.2 Project Success Criteria

**Automated Scheduling Efficiency:**
- Reduce manual scheduling workload by **80–90%** through chatbot-driven appointment creation, modification, and query handling.
- Success measured by the percentage of interactions completed without human intervention.

**System Response Performance:**
- Maintain an end-to-end chatbot response time of **≤ 5 seconds** for 95% of all user messages.
- Measured via CloudWatch metrics and application logs.

**Platform Availability:**
- Achieve **99.9% uptime** using AWS serverless components (Lambda, API Gateway, DynamoDB, RDS).
- Verified through CloudWatch availability dashboards and API Gateway monitoring.
  
**Data Security & Compliance:**
- Enforce secure data handling using IAM least privilege, Cognito authentication, Secrets Manager, VPC isolation, SSM, and VPC Endpoints.
- Compliance validated through IAM Access Analyzer, VPC flow logs, and credential audits.
  
**Operational Dashboard Readiness:**
- Deliver a fully functional Admin Dashboard that allows consultants to monitor schedules, view reports, and manage user sessions.
- Success measured by usability testing and completion of all admin workflows.
  
**Messaging Channel Stability:**
- Provide a stable and error-free integration with Facebook Messenger (webhook error rate <1%).
- Measured via webhook error rate (<1%) and event processing success metrics.
  
**Secure Email Verification:**
- Ensure OTP email verification is reliably delivered through Amazon SES with >98% delivery success.
- Measured using SES delivery reports and bounce/complaint metrics
  
### 1.3 Assumptions
**Prerequisites & Access:**
* AWS Account & Region: Assumes availability of an active AWS account. Target region is **Asia Pacific (Tokyo) - ap-northeast-1** due to Bedrock model availability.
* Meta (Facebook) Account: Assumes client has valid Meta Developer account. Credentials (App ID, Page Token) are stored in AWS SSM/Secrets Manager.
* Email Verification: Sender email for Amazon SES is verified.

**External Dependencies:**
*	Facebook Messenger Platform: The chatbot’s frontend relies entirely on the stability and availability of the Facebook Messenger Graph API (v18.0). Any significant changes to the Facebook Webhook payload structure or API deprecations may require code updates.
*	LLM Availability: The system depends on the continued availability and quota sufficiency of Anthropic Claude 3 Haiku (for chat logic) and Claude 3.5 Sonnet (for Text-to-SQL) within Amazon Bedrock.

**Technical Constraints**
* Language Support: The system prompts and database text search (unaccent extension) are optimized specifically for the Vietnamese language . It is assumed that the primary user base communicates in Vietnamese.
* Data Structure: The project assumes specific CSV file formats (column names, data types) for the initial data import into RDS . Any deviation in the input data schema may cause the initialization or indexing process to fail.
* Serverless Limits: The application logic is constrained by AWS Lambda execution limits (e.g., the Text2SQL and ChatHandler functions have a timeout of 120 seconds). Complex queries or LLM latency exceeding this window may result in timeouts.

**Risks:** 
* LLM Accuracy (Hallucinations): While prompt engineering is used to mitigate errors, it is assumed that there is a non-zero risk of the AI model generating incorrect SQL queries or natural language responses.
* Cost Variance: The project utilizes "pay-as-you-go" services (Bedrock tokens, Lambda invocations). It is assumed the client understands that operational costs will fluctuate based on traffic volume and the complexity of user interactions.
* Data Privacy: Since the database is deployed in a private subnet, it is secure from public access. However, it is assumed that sensitive PII (Personally Identifiable Information) handling complies with the client's internal data governance policies, as the chatbot processes names, phone numbers, and emails.


## 2. SOLUTION ARCHITECTURE

### 2.1 Technical Architecture Diagram

#### 2.1.1 Architecture Description
The proposed solution utilizes a **Serverless-First** and **Event-Driven** architecture hosted on the AWS Cloud (Region: ap-northeast-1), designed to ensure scalability, security, and cost-efficiency compliant with the AWS Well-Architected Framework.

The architecture is divided into three main logical layers:

1. **Frontend & Presentation Layer:** 
   * Admin Dashboard & Consultant Portal: Hosted as Single Page Applications (SPA) on Amazon S3 and distributed globally via Amazon CloudFront (CDN) for low latency.
   * Chat Interface: Integrates directly with the Facebook Messenger Platform via Webhooks.

2. **Processing & Business Logic Layer (VPC-Secured):**
    * **API Gateway:** Serves as the secure entry point for both the Facebook Webhook and Dashboard API calls.
    * **Asynchronous Processing:** To ensure high availability and decoupling, incoming messages are pushed to Amazon SQS (FIFO) before processing. This prevents data loss during traffic spikes and ensures message ordering.
    * **Compute:** AWS Lambda functions handle all business logic, including webhook verification, chat processing, and admin CRUD operations.
    * **AI Integration:** The system leverages Amazon Bedrock via VPC Interface Endpoints to access Foundation Models (Claude 3 Haiku for intent detection, Claude 3 Sonnet for extraction and Claude 3.5 Sonnet for Text-to-SQL generation) securely without traversing the public internet.
3. **Data & Storage Layer:** 
   * **Relational Data:** Amazon RDS for PostgreSQL stores structured data (Consultants, Customers, Appointments). It is deployed in private isolated subnets.
   * **Session Data:** Amazon DynamoDB manages user sessions and conversation context with high-speed read/write capabilities.
   * **Archival:** Amazon S3 is used for storing raw data imports and historical archives via EventBridge scheduled jobs.


#### 2.1.2 Network Infrastructure & Security
* **VPC Isolation:** All core compute (Lambda) and database resources reside in a Virtual Private Cloud (VPC) within Private Isolated Subnets, ensuring no direct exposure to the public internet.
* **VPC Endpoints:** Instead of using NAT Gateways (cost optimization), the architecture uses VPC Gateway Endpoints (for S3, DynamoDB) and Interface Endpoints (for Secrets Manager, Bedrock Runtime) to keep traffic within the AWS network.
* **Authentication:** Amazon Cognito User Pools manage authentication for Admin and Consultant portals. Facebook Messenger validates integrity via HMAC signatures using secrets stored in AWS Secrets Manager.
* **Access Control:** AWS IAM follows the principle of least privilege for all service-to-service interactions.

#### 2.1.3 Data Process Flow

| Step | Flow | Description |
|---|---|---|
| 1 | User → Facebook Messenger | User sends message |
| 2 | FB → API Gateway → WebhookReceiver | Webhook receives & validates event |
| 3 | WebhookReceiver → SQS | Message queued for async processing |
| 4 | SES → User | Send OTP via email |
| 5 | ChatHandler → DynamoDB | Store session & conversation cache |
| 6 | ChatHandler → Claude 3 Haiku | Intent detection |
| 7 | Claude 3 Haiku → Claude 3 Sonnet | Analyze context, user info (INSERT/UPDATE sched.) |
| 8 | Text2SQL Handler → VPC Endpoint → Claude 3.5 Sonnet | Natural language → SQL (SELECT + INSERT/UPDATE) |
| 9 | Text2SQL Handler → PostgreSQL | Execute SQL |
| 10 | SES → Consultant | Notify consultant |
| 11 | AdminManager → PostgreSQL | Admin data management |
| 12 | EmailHandler → SES | Send appointment updates |
| 13 | EventBridge | Trigger daily job |
| 14 | ArchiveData → S3 | Store historical data |

#### 2.1.4 Architecture Diagram

![Chatbot Architecture](/images/2-Proposal/chatbot_final_final_final.drawio.png)

#### 2.1.5 Tools & Services List
**AWS Services:**
*  Compute: AWS Lambda
*	API: Amazon API Gateway
*	Database: Amazon RDS (PostgreSQL), Amazon DynamoDB
*	AI/ML: Amazon Bedrock (Claude 3 Haiku, Claude 3 Sonnet, Claude 3.5 Sonnet, Titan Embeddings)
*	Storage: Amazon S3
*	Networking: Amazon VPC, VPC Endpoints (Gateway & Interface)
*	Content Delivery: Amazon CloudFront
*	Auth: Amazon Cognito
*	Messaging/Queues: Amazon SQS (FIFO), Amazon SES
*	Orchestration: Amazon EventBridge
*	Management: AWS CloudFormation (via CDK), Systems Manager (SSM), Secrets Manager, CloudWatch

**Development Tools:**
* IaC: AWS Cloud Development Kit (CDK) v2 (Python)
* Languages: Python 3.12 (Backend), TypeScript/React (Frontend)
* Containerization: Docker (for building Lambda layers) 
* Version Control: Git

### 2.2 Technical Plan
**Infrastructure as Code (IaC) & Deployment** 

The development team will develop scripts using **AWS Cloud Development Kit (CDK) v2** with Python 3.12. This will allow for quick and repeatable deployments into AWS accounts using standard cdk deploy commands. The entire infrastructure (VPC, Lambda, RDS, DynamoDB, API Gateway, Cognito) is defined in code, ensuring consistency across development, testing, and production environments.

**Configuration & Approvals**

Some additional configuration such as **Amazon Bedrock Model Access** (specifically for Anthropic Claude 3 Haiku and Claude 3.5 Sonnet), **Facebook App Review** (for pages_messaging permission), and **Amazon SES Production Access** (to move out of the sandbox environment) may require approval and will follow these processes:

**Testing Strategy**

All critical paths will include extensive coverage, specifically:
* Unit Testing: For individual Lambda functions (ChatHandler, Text2SQL) and utility modules.
* Integration Testing: Verifying the end-to-end flow from Facebook Messenger → API Gateway → SQS → SES →  Lambda → Bedrock → RDS.
* Security Testing: verifying IAM least privilege roles and VPC security group rules.

### 2.3 Project Plan (Agile Scrum)

| Month | Phase | Key Deliverables |
|---|---|---|
| **September** | AWS Learning & Lab Practice | AWS Serverless fundamentals (Lambda, API Gateway, RDS, DynamoDB, S3), Building basic serverless applications, AWS IAM & security best practices |
| **October** | Advanced AWS & Infrastructure Setup | Advanced AWS services deep-dive (MemoryDB, Bedrock, VPC, CDK), Initial infrastructure deployment (RDS, DynamoDB, Lambda layers), AWS CDK IaC templates & automation |
| **November** | Research, Architecture & Development | System architecture design (ChatHandler, SQL Module, RAG Module), Core feature development, ChatHandler implementation, SQL Text-to-SQL handler, ScheduleExecutor & Admin Dashboard, Bedrock integration & LLM prompt engineering |
| **December** | Testing, Optimization & Deployment | End-to-end integration testing, Performance optimization & load testing, Demo preparation, Final deployment, Project documentation & handover |

### 2.4 Security Considerations
The solution implements a "Security by Design" approach, leveraging AWS native security services and best practices to ensure data integrity, confidentiality, and availability. Security measures are categorized into five key domains:
1.  **Access (Identity & Access Management)** 
      *	IAM Least Privilege: All AWS Lambda functions operate with granular IAM roles that grant only the minimum necessary permissions (e.g., specific DynamoDB table access, restricted Bedrock model invocation), adhering to the principle of least privilege.
      *	User Authentication: Secure authentication for the Admin Dashboard and Consultant Portal is managed via Amazon Cognito User Pools, ensuring centralized identity management and secure token handling.
      *	Webhook Validation: All incoming requests from Facebook Messenger are validated using HMAC-SHA256 signature verification (X-Hub-Signature-256) to ensure message integrity and origin authenticity.
      *	End-User Verification: A secure OTP (One-Time Password) mechanism via Amazon SES is implemented to verify the identity of chat users before processing sensitive booking requests.

2.  **Infrastructure (Network & Compute Security)** 
      * Network Isolation: All backend compute resources (Lambda) and databases (Amazon RDS) are deployed within VPC Private Isolated Subnets, with no direct ingress from the public internet.
      *	VPC Endpoints: Communication between AWS services (Lambda to Bedrock, Secrets Manager, S3, DynamoDB) occurs privately via VPC Interface and Gateway Endpoints, keeping traffic entirely within the AWS network backbone.
      *	Encryption in Transit: All network traffic is encrypted using TLS 1.2+ via Amazon API Gateway and CloudFront.

3.  **Data (Protection & Privacy)** 
      *	Secrets Management: Sensitive credentials (database passwords, Facebook Page Tokens) are stored and retrieved securely from AWS Secrets Manager and SSM Parameter Store. No secrets are hardcoded in the application source code.
      *	SQL Injection Prevention: The Text-to-SQL layer implements strict guardrails, including:
         *	Use of parameterized queries (via psycopg) to neutralize injection attacks.
         *	LLM output validation to strictly match database schema parameters.
         *	Authorization layers to restrict database mutations (INSERT/UPDATE) based on user intent.

4.  **Detection (Logging & Monitoring)** 
      *  Centralized Logging: Application logs, error traces, and access logs are aggregated in Amazon CloudWatch Logs for real-time analysis and troubleshooting
5.  **Incident Management:**
      *	Resilience & Failover: The system includes built-in handling for service throttling (e.g., Bedrock rate limits) and exponential backoff retry mechanisms to maintain stability during incidents.

---

## 3. ACTIVITIES AND DELIVERABLES

### 3.1 Activities and deliverables

| Project Phase | Timeline | Activities | Deliverables | Effort (M/D) |
|---|---|---|---|---|
| **AWS Learning & Hands-On** | September – October (8 weeks) | AWS fundamentals practice (Lambda, API Gateway, RDS, DynamoDB); Infrastructure planning; Architecture design | CCompletion of core AWS labs; Technical architecture; Infrastructure design document | 120 |
| **Research & Development** | Early November – Mid November (2 weeks) | Finalize system architecture; Design SQL module; Confirm technology stack | Detailed system architecture diagram; Module specifications; Technology selection report | 30 |
| **Core System Development** | Mid November – Late November (2.5 weeks) | BBuild WebhookReceiver; Develop ChatHandler; Text-to-SQL module; Session management; Integrate Amazon Bedrock | WebhookReceiver service; ChatHandler with scheduling logic; Text-to-SQL processor; Fully working chatbot | 12.5 |
| **Infrastructure Deployment** | Mid November – Late November (2 weeks) | Set up VPC; Deploy Lambda, RDS/DynamoDB; Configure Secrets Manager; Set up API Gateway | Deployed AWS infrastructure; Lambda functions; Databases; Security groups configured | 30 |
| **Admin Dashboard/Consultant Portal & Features** | Late November – Early December (2 weeks) | Frontend Dashboard (React/TypeScript); Analytics page; Counselor management; Admin scheduling; Counselor scheduling | Fully functional admin dashboard/consultant portal; UI components; Charts and data visualizations | 25 |

### 3.2 OUT OF SCOPE
**Communication Channel Integrations**
*	Multi-channel integrations beyond Facebook Messenger (e.g., WhatsApp, Line, Telegram, website chat widget)
*	Voice call or IVR-based customer support integrations
*	AI/ML Enhancements
*	RAG (Retrieval-Augmented Generation) module using external knowledge bases
*	Fine-tuning or customizing LLM models beyond the standard Amazon Bedrock offerings

**Infrastructure**
*	Multi-region failover and disaster recovery implementation
*	Advanced cost-optimization strategies or capacity forecasting management

**Analytics & Reporting**
*	Predictive analytics for consultation trends
*	Integration with BI platforms (Tableau, Power BI)

### 3.3 PATH TO PRODUCTION
The Proof of Concept (POC) is architected to demonstrate the core value proposition of the Intelligent Scheduling Chatbot using a serverless-first approach on AWS. While the POC establishes a functional end-to-end booking flow via Facebook Messenger, it is scoped to validate technical feasibility and user experience rather than to support high-concurrency production workloads immediately.

**Current POC Capabilities & Focus**: The current release focuses on the following targeted use-cases and technical validations:

*	Core Integration: Seamless bi-directional integration with Facebook Messenger via Webhooks and Graph API.
*	Architecture Validation: Validation of the AWS Serverless stack (Lambda, API Gateway, DynamoDB, RDS) for cost-efficiency and event-driven processing.
*	AI Logic: Implementation of Text-to-SQL capabilities using Amazon Bedrock (Claude 3.5 Sonnet) to accurately query availability and modify schedule data securely.
*	Management Interfaces: A functional Admin Dashboard and Consultant Portal for real-time schedule management and user oversight.
*	Performance: Initial optimization of cold starts and LLM response latency to ensure acceptable user experience.

**Gap Analysis & Production Roadmap**: To transition from the current POC to a fully resilient, enterprise-grade production system, the solution requires further investment in operational excellence, multi-channel support, and advanced analytics. The following roadmap outlines the key phases to address these gaps:
*	Phase 2 - Omni-channel Expansion: Extend the chatbot interface beyond Facebook Messenger to include a Web Widget (for corporate websites) and a dedicated Mobile Application, ensuring a unified customer experience across touchpoints.
*	Phase 3 - AI Cost & Performance Optimization: Transition from general-purpose Foundation Models to Small Language Models (SLMs) fine-tuned specifically for SQL generation tasks. These models will be hosted on Amazon EC2/SageMaker to reduce inference latency and operational costs at scale.
*	Phase 4 - Advanced Data Analytics: Implement an AWS Glue + Amazon Athena pipeline to perform deep analytics on conversation logs and booking trends, enabling data-driven business decisions beyond simple operational reporting.
*	Phase 5 - Operational Excellence & Scalability: Deploy comprehensive auto-scaling strategies across all layers to handle fluctuating traffic loads dynamically. This includes Provisioned Concurrency for Lambda functions to eliminate cold starts, storage auto-scaling for RDS, and EC2 Auto Scaling Groups for the fine-tuned LLM inference fleet. Additionally, enhance observability by implementing AWS X-Ray distributed tracing and custom CloudWatch dashboards for proactive anomaly detection and incident management.
*	Phase 6 - High Availability & Disaster Recovery: Implement Multi-region deployment (Active-Passive) to ensure business continuity and 99.99% availability in the event of a regional service disruption.
---

## 4. EXPECTED AWS COST BREAKDOWN

**Region:** ap-northeast-1 (Tokyo) | **Source:** [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=ee545a5e20d05d16fbf6eab1e4e66a35b70a2323) | Estimate Date: 8 December 2025 

| AWS Service | Monthly Cost (USD) | 12 Months Cost | Description / Configuration |
|---|---|---|---|
| **Amazon VPC** | $20.45 | $245.40 | Network Security: 2 VPC Interface Endpoints (PrivateLink) to secure traffic between Lambda, Bedrock, and Secrets Manager. |
| **Amazon Bedrock** | $9.08 | $108.96 | Generative AI Models: Combined cost for Claude 3 Haiku (Chat/Intent), Claude 3 Sonnet (Context Analysis), and Claude 3.5 Sonnet (Text2SQL).  |
| **Amazon RDS** | $5.83 | $69.96 | Database: db.t3.micro, 20 GB GP2 Storage, Single-AZ deployment, est. 15% utilization/month. |
| **Amazon Cognito** | $0.50 | $6.00 | 10 MAU with Advanced Security. |
| **Amazon SQS** | $0.50 | $6.00 | FIFO Queue, 1M requests/month. |
| **AWS Secrets Manager** | $0.40 | $4.80 | Security: 1 secret stored, automatic rotation enabled (30-day interval). |
| **Amazon DynamoDB** | $0.28 | $3.36 | On-Demand, 1 GB storage. |
| **Amazon CloudFront** | $0.12 | $1.44 | CDN: 1 GB data transfer out, 1,000 HTTPS requests/month. |
| **Amazon SES** | $0.05 | $0.60 | Email Service: Est. 10 emails processed/day (OTP & Notifications). |
| **Amazon S3** | $0.03 | $0.36 | 1 GB Standard storage. |
| **API Gateway** | $0.00 | $0.00 | Covered by AWS Free Tier (est. 1,000 requests/month). |
| **AWS Lambda** | $0.00 | $0.00 | Covered by AWS Free Tier (est. 100 requests/month). |
| **EventBridge** | $0.00 | $0.00 | Covered by AWS Free Tier (est. 10 custom events/month). |
| **TOTAL** | **$37.24** | **$446.88** | **Upfront: $0.00** |

**Assumptions & Cost Optimization Strategies**
1.	**Bedrock Model Specifics**: The AWS Pricing Calculator uses generic identifiers for Bedrock models. This proposal specifically utilizes Anthropic Claude 3 Haiku for low-latency intent detection, Claude 3 Sonnet for reasoning/context, and Claude 3.5 Sonnet for complex Text-to-SQL generation. The estimated cost reflects a blended usage of these models for demonstration purposes.
2.	**VPC Endpoint Optimization**: VPC Interface Endpoints currently account for ~55% of the estimated monthly cost ($20.45). As this is a Proof of Concept (POC), these endpoints can be de-provisioned when not in active testing to significantly reduce actual costs.
3.	**AI Model Usage**: Bedrock costs are variable based on token consumption. The estimate assumes moderate testing traffic; production costs will scale linearly with actual user volume.
4.	**Instance Utilization**: The RDS instance (db.t3.micro) is estimated at 15% utilization. For development environments, the database can be stopped outside of business hours to save approximately 60-70% of the RDS hourly cost.
5.	**Free Tier Leveraging**: The architecture maximizes the use of AWS Free Tier for compute (Lambda), API management (API Gateway), and orchestration (EventBridge) to keep the baseline operational cost minimal.


---

## 5. TEAM

### Customer Executive Sponsor & Stakeholders
| Name | Title | Role / Responsibilities | Email / Contact Info
|---|---|---| ---|
| **Nguyen Gia Hung** | Head of Solutions Architect (AWS FCJ Lead) | Executive Sponsor & Mentor: Acts as the primary technical advisor, providing high-level architectural validation, strategic mentorship, and ensuring the solution adheres to AWS best practices. | hunggia@amazon.com |
| **AWS FCJ Mentors** | Program Instructors | Project Stakeholders: Responsible for academic governance, evaluating project deliverables against program standards, and approving internship credits. | FCJ – FPTU Channel |

### Partner Project Team
| Name | Role | Responsibilities | Email / Contact Info |
|---|---|---|---|
| **Phan Quoc Anh** | Technical Lead / Full-stack | **Solutions Architect (Co-Lead):** Co-designed AWS serverless architecture. Leads the AI & Chatbot Stream (Bedrock integration, Text2SQL logic, ChatHandler). Responsible for technical feasibility reviews. | pqa1085@gmail.com  0379729847 |
| **Dang Truong Hung** | Full-stack Engineer | **Developer & QA:** Co-designed AWS serverless architecture. Key contributor to the Application & Dashboard Stream. Responsible for end-to-end implementation of the Admin Dashboard (Frontend) and complex Lambda business logic (Backend). Leads system Quality Assurance (QA), testing | fptutruonghung@gmail.com 0937726869 |
| **Hoang Le Thanh Duc** | PM / Full-stack | **Solutions Architect (Co-Lead):** Co-designed AWS serverless architecture. Leads the Application & Dashboard Stream (Admin Dashboard, Consultant Portal, Backend Logic). Responsible for project coordination and progress tracking. | fptuduchoang@gmail.com 0829497169 |

---

## 6. RESOURCES & COST ESTIMATES

| Resource | Responsibility | Rate (USD) / Hour |
|---|---|---|
| Solution Architects <span style="background-color: yellow;">[2]</span> | System Architecture Design, Security Planning, Technology Selection, Technical Review | $0 |
| Engineers <span style="background-color: yellow;">[3]</span> | Full-stack Development, Infrastructure Deployment (IaC), Testing, Quality Assurance | $0 |
| Other (Please specify) | | $0 |


<span style="background-color: yellow;">* Note: Refer to section "activities & deliverables" for the list of project phases</span>

| Project Phase | Solution Architects (Hours) | Engineers (Hours) | Total Hours |
|---|---|---|---|
| AWS Learning & Hands-On Practice | 320 | 640 | 960 |
| Research & Development | 140 | 100 | 240 |
| Core System Development | 20 | 80 | 100 |
| Infrastructure Deployment | 80 | 160 | 240 |
| Admin Dashboard/Consultant Portal | 40 | 160 | 200 |
| **Total Hour** | **600** | **1,140** | **1,740** |
| **Total Cost** | $0$ | $0 | $0 |


Cost Contribution distribution between Partner, Customer, AWS:

| Party | Contribution (USD) | % Contribution of Total |
|---|---|---|
| Customer | $0 | $0 |
| Partner | $0 | $0 |
| AWS | $600 | 100% |

---

## 7. ACCEPTANCE

### 7.1	EVALUATION PROCESS
As this is a Proof of Concept (POC) project within the framework of the training program, the acceptance process will focus on demonstrating the feasibility of the solution:
1.  **Deployment & Internal Testing:** The project team performs self-testing to ensure core workflows function correctly in the AWS environment.
2.  **Official Demo:** The team performs a live demonstration of the committed use-cases to the Mentor/Instructors.
3.  **Feedback:** Receive feedback from the Mentor regarding functionality and architecture.
4.  **Finalization:** Fix critical bugs (if any) that affect the core flow and submit the final report.

### 7.2	ACCEPTANCE CRITERIA
The project is considered complete when it meets the following basic functional criteria (minor UI bugs or unhandled edge cases are acceptable):

**1. AWS Infrastructure:**
*   The system is successfully deployed on AWS (not running locally).
*   Key services (Lambda, RDS, Bedrock) are successfully connected.

**2. Chatbot Functionality (Core Flow):**
*   **Happy Path:** The chatbot can successfully execute an end-to-end booking process (Inquire → Check Availability → Book → Save to DB) under normal network conditions.
*   **Response:** The chatbot provides relevant answers (within the capabilities of the current AI model).

**3. Admin Dashboard / Consultant Portal:**
*   Accessible via the CloudFront/S3 URL.
*   Successful login with an Admin account and Consultant account.
*   Displays appointment data from the database (minor latency is acceptable).

**4. Documentation:**
*   Full Source Code provided on GitHub.
*   Setup guide (Readme) and project architecture report.

---
Download full proposal document: [MeetAssist Intelligent Scheduling Chatbot](/images/2-Proposal/Proposal_Template.docx)