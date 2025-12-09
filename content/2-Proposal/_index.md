---
title: "Proposal"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Intelligent Scheduling Chatbot on AWS
## A Serverless Solution for Automated Appointment Booking & Support
[![Download MeetAssist Chatbot Proposal](https://img.shields.io/badge/MeetAssist_Chatbot_Proposal-Click_Here-0056D2?style=for-the-badge&logo=google-docs&logoColor=white)](/images/2-Proposal/Proposal_Template.docx)

### 1. Executive Summary
The Intelligent Scheduling Chatbot on AWS is a fully serverless solution designed to automate appointment booking and customer support through Facebook Messenger. The system integrates Large Language Models (LLMs) on Amazon Bedrock (Claude 3.5 Sonnet, Claude 3 Haiku, Claude 3 Sonnent) using a Text-to-SQL mechanism to query/execute SQL on a PostgreSQL database. It ensures accurate, context-aware responses and reduces manual scheduling workload by 80–90% while maintaining enterprise-grade security within the Asia Pacific (Tokyo) region.

### 2. Problem Statement
### What’s the Problem?
Manual appointment scheduling creates a significant workload for staff, leading to inefficiencies and delayed response times. There is a lack of automated handling for complex queries (e.g., checking specific availability or modifying bookings), and existing support channels often suffer from human error or unavailability outside business hours.

### The Solution
The platform uses **Amazon Bedrock** to leverage Foundation Models (Claude 3 Family) for intent detection and Text-to-SQL generation. **AWS Lambda** and **Amazon API Gateway** handle business logic and Facebook Webhook integration. **Amazon RDS (PostgreSQL)** stores structured appointment data, while **Amazon DynamoDB** manages session context. **Amazon SES** provides secure OTP verification. The system offers an Admin Dashboard hosted on **Amazon S3** and **CloudFront** for consultants to manage schedules efficiently.

### Benefits and Return on Investment
The solution reduces manual scheduling effort by **80–90%** and ensures an end-to-end response time of **≤ 5 seconds**. It provides **99.9% uptime** through serverless architecture and ensures strict data security via VPC isolation and Cognito authentication. The estimated monthly cost is **$37.24 USD**, providing a cost-effective, pay-as-you-go model that scales with traffic, eliminating the need for expensive fixed-server infrastructure.

### 3. Solution Architecture
The platform employs a **Serverless-First** and **Event-Driven** architecture hosted in the ap-northeast-1 region. Incoming messages are buffered via Amazon SQS before being processed by Lambda functions that interact with Amazon Bedrock for AI logic and RDS for data persistence. The architecture is detailed below:

![Chatbot Architecture](/images/2-Proposal/chatbot_final_final_final.drawio.png)

### AWS Services Used
- **Amazon Bedrock**: Access to Claude 3 Haiku (Intent), Claude 3 Sonnet (Context), and Claude 3.5 Sonnet (Text2SQL).
- **AWS Lambda**: Handles ChatHandler, Text2SQL logic, and Webhook processing.
- **Amazon API Gateway**: Secure entry point for Facebook Webhooks and Dashboard APIs.
- **Amazon RDS (PostgreSQL)**: Stores consultants, customers, and appointment data.
- **Amazon DynamoDB**: Manages user sessions and conversation context cache.
- **Amazon SQS (FIFO)**: Queues incoming messages for asynchronous processing.
- **Amazon SES**: Sends emails to users.
- **Amazon Cognito**: Manages authentication for the Admin Dashboard.

### Component Design
- **Frontend Layer**: Facebook Messenger via Webhook and an Admin Dashboard (React) hosted on S3/CloudFront.
- **Processing Layer**: Lambda functions execute business logic; SQS ensures message ordering; Bedrock handles AI reasoning.
- **Data Layer**: RDS for relational data (private subnet); DynamoDB for high-speed session retrieval.
- **Security**: VPC Endpoints for private communication; Secrets Manager for credentials; IAM least privilege enforcement.
- **User Management**: Amazon Cognito for staff; Facebook Messenger HMAC signature for end-users.

### 4. Technical Implementation
**Implementation Phases**
This project follows an Agile Scrum methodology divided into 4 key phases:
- **AWS Learning & Lab Practice**: Focus on Serverless fundamentals (Lambda, API Gateway, RDS) and IAM security (September – October).
- **Research & Development**: Finalize Text-to-SQL architecture, select Bedrock models, and design the SQL schema (Early November).
- **Core System Development**: Build WebhookReceiver, ChatHandler, Text-to-SQL module, and integrate Amazon Bedrock (Mid – Late November).
- **Infrastructure & Dashboard**: Deploy VPC/Infrastructure via CDK, develop the Admin Dashboard, and perform end-to-end testing (Late November – December).

**Technical Requirements**
- **Core Stack**: Python 3.12 (Backend), TypeScript/React (Frontend), AWS CDK v2 (IaC).
- **AI/ML Requirements**: Access to Anthropic Claude 3 Haiku, Claude 3.5 Sonnet, Claude 3 Sonnent and Amazon Titan Embeddings G1 via Amazon Bedrock.
- **Database**: PostgreSQL with `unaccent` extension for Vietnamese language support; CSV data imports for initialization.
- **External Dependencies**: Meta (Facebook) Developer Account for Graph API v18.0; Verified Amazon SES identity.

### 5. Timeline & Milestones
**Project Timeline**
- **September – October**: AWS Learning & Hands-On Labs.
- **Early November**: Architecture Design & Technology Selection.
- **Mid November**: Core Backend Development (ChatHandler, SQL Module).
- **Late November**: Infrastructure Deployment & Admin Dashboard Frontend.
- **December**: Integration Testing, Optimization, and Final Presentation.

### 6. Budget Estimation
You can find the budget estimation on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=ee545a5e20d05d16fbf6eab1e4e66a35b70a2323).

### Infrastructure Costs
- **AWS Services:**
    - **Amazon VPC**: $20.45/month (2 Interface Endpoints for security).
    - **Amazon Bedrock**: $9.08/month (Tokens for Claude 3 Haiku/Sonnet and Claude 3.5 Sonnent models).
    - **Amazon RDS**: $5.83/month (db.t3.micro, 20GB storage).
    - **Amazon Cognito**: $0.50/month (10 MAU).
    - **Amazon SQS**: $0.50/month (1M requests).
    - **AWS Secrets Manager**: $0.40/month.
    - **Amazon DynamoDB**: $0.28/month (On-demand).
    - **Amazon SES & S3**: <$0.10/month.
    - **API Gateway, Lambda, EventBridge**: $0.00 (Covered by Free Tier).

**Total**: $37.24/month, ~$446.88/12 months.

### 7. Risk Assessment
#### Risk Matrix
- **LLM Accuracy (Hallucinations)**: Medium impact, medium probability.
- **Cost Variance**: Low impact, medium probability (Pay-as-you-go fluctuations).
- **Data Privacy**: High impact, low probability.
- **SQL Generation Failure**: High impact, medium probability.
- **Insufficient Context (Contextual Awareness)**: High impact, low probability.
- **OTP Brute-force Attack**: High impact, low probability.

#### Mitigation Strategies
- **Accuracy**: Strict prompt engineering and database user permission guardrails (SELECT/INSERT only).
- **Cost**: VPC Endpoint optimization (remove when idle) and Free Tier usage.
- **Privacy**: Database in Private Isolated Subnets; PII compliance governance.
- **SQL Generation**: Prompt validation is strictly implemented to handle enum constraints, verify column/table names, and correctly format `WHERE` clauses (including `LIKE` operators) for Vietnamese names/text.
- **Context**: System prompts include mandatory function calls to retrieve additional session context, ensuring the LLM fully understands the user's message history before responding.
- **OTP Security**: Rate limiting is enforced (max 5 attempts/session, 15s cooldown), with auto-blocking for 3600s after failures. OTPs expire in 5 minutes, and verification uses HMAC timing-attack safe methods.


### 8. Expected Outcomes
#### Technical Improvements:
Automated, context-aware scheduling via SQL generation.
End-to-end response latency ≤ 5 seconds.
Secure, VPC-isolated infrastructure with 99.9% uptime.

#### Long-term Value
Scalable foundation for omni-channel expansion (Web/Mobile).
Data collection for future advanced analytics (AWS Glue/Athena).
Operational excellence through reduced manual administrative work.