---
title: "Proposal"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI-Powered Booking Chatbot on AWS
## AWS Serverless solution with RAG and SQL-Driven workflows for booking and customer care

### 1. Executive Summary  
The AI-Powered Booking Chatbot on AWS is an intelligent chatbot solution designed to assist users with booking appointments and looking up service information via Facebook Messenger. The system leverages LLMs combined with Retrieval-Augmented Generation (RAG) and a SQL-driven model to handle natural conversations while retrieving accurate data from PostgreSQL and DynamoDB. The platform uses an AWS Serverless architecture to reduce operational costs, scale automatically, and ensure reliability.

### 2. Problem Statement  
Current problems  
Most existing chatbot solutions are limited to answering general service questions. Booking is still often handled manually (messages or phone calls) and is not fully automated, which reduces flexibility, efficiency, and accuracy as user volume grows. Deploying AI chatbots can be complex without a flexible cloud platform to manage data, conversation flows, and security.

Solution  
The project uses AWS Lambda, API Gateway, DynamoDB, PostgreSQL, and AI-supporting services to build a versatile chatbot capable of:
  - Integrating with Messenger with a simple, accessible interface.
  - Analyzing conversational intents (booking, consultation, general questions).
  - Connecting to databases to retrieve schedules, customer information, or analytics data.
  - Supporting a RAG module for open-ended questions or complex contexts.
  - Providing an Admin Dashboard to monitor conversation history, statistics, and system performance.

Benefits and ROI  
The solution aims to automate 80–90% of booking workflows and operate 24/7, reducing operational and personnel costs compared to on-premises infrastructure. It also provides practical learning for students/research teams on AWS Serverless, NLP, and RAG. The system is reusable and extensible for SMEs.

### 3. Solution Architecture  
Overview  
The platform runs Serverless with VPC security; all conversation processing, scheduling, and AI data are handled by AWS Lambda and other serverless services.

![Chatbot Architecture](/images/2-Proposal/chatbot_final_final.drawio.png)

Main data flow
1. User chats via Facebook Messenger → API Gateway → Lambda WebhookReceiver (validation, authorization).
2. Lambda ChatOrchestrator calls the Intent Model to process intent and routes to the SQL module or RAG Module.
3. DynamoDB stores conversation cache and metadata, while PostgreSQL stores booking records and history.
4. EventBridge manages jobs to archive booking data from PostgreSQL to S3 daily for the Admin Dashboard.
5. Admin Dashboard (Route 53 + CloudFront + S3 + Cognito) enables admins to monitor, test, analyze, and manage the system securely.

AWS services used
- AWS Lambda: conversation processing, intent orchestration, scheduling.
- Amazon API Gateway: connects Messenger and the Admin Dashboard.
- Amazon DynamoDB: cache, logs, metadata for RAG and short-term memory.
- Amazon RDS (PostgreSQL): booking records and interaction history.
- Amazon EventBridge: event management and cron jobs.
- Amazon S3 + CloudFront + Route 53: host and distribute the Admin UI.
- Amazon Cognito: user management and admin authorization.
- AWS Secrets Manager: secure storage for service credentials.
- AWS Glue + Athena (optional analytics): extract and analyze historical conversation data.
- Amazon Bedrock: intent analysis, entity extraction, and context-aware response generation.
- Amazon CloudWatch: logging and monitoring.

### 4. Technical Deployment  
Deployment stages  
The project has two parts — building the chatbot system and the AI Booking Admin platform — each following four main stages:

1. Research and architecture design  
   - Analyze chatbot models integrating RAG and intent classification.  
   - Propose an AWS Serverless architecture: Lambda, API Gateway, RDS PostgreSQL, DynamoDB, EventBridge.  
   - Evaluate Foundation Models on Amazon Bedrock (e.g., Claude 3, Llama 2).  
   - Research CI/CD with AWS CDK or CloudFormation for automated deployment.  
   - (Pre-workshop: prepare technical environment and architecture diagrams.)

2. Cost estimation and feasibility testing  
   - Use AWS Pricing Calculator to estimate infrastructure costs (Lambda, RDS, DynamoDB, Amplify, Cognito, EventBridge, S3, CloudFront).  
   - Run small sandbox tests to validate scalability, response time, and stability.  
   - (Early workshop: use findings to tune resources and sizing.)

3. Architecture refinement and optimization  
   - Balance cost and performance: optimize Lambda usage and reduce RDS costs using caching (DynamoDB).  
   - Separate conversation flows for "Booking" and "Customer Service" intents to reduce processing overhead and LLM cost.  
   - Test scalability and stability under increased concurrent users.  
   - (Mid-workshop: ensure cost-effective and technically optimized system.)

4. Development, testing, and deployment  
   - Develop core Lambdas (WebhookReceiver, ChatOrchestrator, RAG Module, ScheduleExecutor, ArchiveData, Admin Manager) and integrate RDS and DynamoDB.  
   - Configure API Gateway, EventBridge, and Cognito; build the Admin UI in JavaScript.  
   - Perform end-to-end testing: Messenger → API Gateway → Chatbot → Database → Dashboard.  
   - (End of workshop: operate the system, record results, and deliver final demo.)

Technical requirements  
- Core platform: AWS Serverless (Lambda, API Gateway, DynamoDB, RDS PostgreSQL, EventBridge).  
- Security: Amazon Cognito, AWS Secrets Manager, segregated IAM Roles.  
- Development: AWS CDK/SDK, JavaScript for the Admin UI.  
- External integration: Facebook Messenger Webhook (API Gateway endpoint).  
- Automation: CloudFormation templates.

### 5. Roadmap & Milestones  
- Internship (Sep–Dec):  
  - Sep: Learn AWS, solidify serverless architecture, build prototype.  
  - Oct: Design and refine architecture.  
  - Nov: Develop and test the system.  
  - Dec: Full deployment, demo, and evaluation.  
- Post-deployment: further research and improvements over 12 months.

### 6. Budget Estimate  
- Download the budget estimate report (PDF): [Budget Estimate - PDF](/images/2-Proposal/chatbotestimation.pdf)

### Estimated Cost Breakdown

- Amazon Virtual Private Cloud (VPC): $57.04 — 6 VPC Interface endpoints per AWS region.
- Amazon Bedrock: $16.38 — 1 request/min, 8 hours/day, 100 input tokens/request, 50 output tokens/request.
- AWS Web Application Firewall (WAF): $9.06 — 1 Web ACL, 3 Rules/Web ACL, 1 Managed Rule Group/Web ACL (monthly).
- Amazon RDS for PostgreSQL: $7.87 — 1 db.t3.micro node (25% utilization/month), 20 GB (General Purpose SSD gp2), Single-AZ, On-Demand.
- Amazon EventBridge: $1.00 — 1 million custom events/month (1 KB payload), 1 million invocations/month.
- Amazon DynamoDB: $0.96 — 1 GB storage, 1 KB average item size, Table class: Standard.
- AWS Glue: $0.54 — 2 DPUs (Apache Spark), 0.0625 DPUs (Python Shell), 1 crawler.
- Amazon Athena: $0.45 — 30 queries/day, 0.1 GB data scanned/query.
- Amazon CloudFront: $0.24 — 1 GB data transfer out (internet)/month, 100,000 HTTPS requests/month.
- Amazon Simple Storage Service (S3): $0.13 — 5 GB S3 Standard storage/month.
- Amazon API Gateway: $0.13 — Estimated 0.1 requests/month.
- AWS Lambda: $0.00 — 10,000 requests/month.
- Total: $93.80

*Important note*: The figures above were calculated using the AWS Pricing Calculator and represent initial estimates. Actual deployment costs may be lower due to (1) actual usage being below configured estimates, (2) Free Tier benefits, and (3) cost optimizations (e.g., caching, Lambda tuning) applied during operation.

### 7. Risk Assessment

| Risk | Impact | Probability | Mitigation |
|---|---:|---:|---|
| Messenger webhook outage | Medium | Medium | Implement retry logic and log monitoring with CloudWatch. |
| Incorrect Lambda permissions | High | Low | Use dedicated IAM roles and test least-privilege permissions. |
| DynamoDB data congestion | Medium | Low | Apply TTL limits and local caching. |
| Cost overrun | Medium | Medium | Monitor AWS Billing Alerts and enable Budget notifications. |

### 8. Expected Outcomes  
- Technical: Deliver a working AI chatbot capable of booking via Messenger and automatically answering customer queries.  
- Academic: Workshop participants understand how to design an AWS Serverless architecture integrated with RAG.  
- Practical: Scale the model into an enterprise chatbot and combine conversation analytics with Glue & Athena.  
- Long-term value: Lay the foundation for an internal Customer Service AI platform or a SaaS product.