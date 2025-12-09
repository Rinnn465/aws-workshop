---
title : "Introduction"
date :  "2025-09-09" 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

#### Problem Statement
Manual booking systems or traditional chatbots often encounter difficulties when the customer volume increases, resulting in poor user experience and higher staffing costs for page management. This workshop addresses the issue by building an architecture capable of:

- **Automation**: Handling booking, rescheduling, and cancellation 24/7.

- **Context understanding**: Accurately identifying user intents.

- **Data retrieval**: Responding to complex questions about available time slots and consultant information.
#### Solution Architecture
The system is designed using an **Event-Driven Serverless** model combined with **VPC-secured** networking to ensure security and scalability:

1. **Frontend Interface**: Users interact via Facebook Messenger.

2. **Request Handling**:

    * Amazon API Gateway receives Webhooks from Facebook.

    * AWS Lambda (WebhookReceiver) sends messages to an Amazon SQS (FIFO) queue to guarantee ordering and asynchronous processing.

3. **Brain (Processing Core):**
    * ChatHandler Lambda: Manages conversations and checks sessions from Amazon DynamoDB.

    * Authentication: User verification through Email OTP using Amazon SES.

4. **AI & Data Layer:**

    * Amazon Bedrock: Uses Claude 3 Haiku (for Intent Classification), Claude 3.5 Sonnet, and Claude 3 Sonnet (for Text-to-SQL & Extraction).
    * Amazon RDS (PostgreSQL): Stores business data (Appointments, Customers, Consultants).

    * Text2SQL Handler: Converts natural language questions into safe SQL queries to retrieve data.

5. **Admin Dashboard & Consultant Portal:** A management interface (ReactJS) hosted on Amazon S3 and delivered through CloudFront, allowing administrators to view statistics and manage appointments. Consultant Portal provides the ability to manage booked appointments with customers and view personal schedules.

![Architecture Diagram](/images/2-Proposal/chatbot_final_final_final.drawio.png)
*(The image illustrates the overall architecture from the Proposal)*


#### Key Technologies

In this workshop, you will work with the following core AWS services:

+ **Amazon Bedrock**: The AI engine, providing Foundation Models (Claude, Titan) for language processing and SQL generation.

+ **AWS Lambda & API Gateway**: Serverless backend without managing servers.

+ **Amazon RDS (PostgreSQL) + pgvector**: Relational database with integrated vector search for RAG.
+ **Amazon DynamoDB**: High-speed storage for session and conversation context.

+ **Amazon SQS**: Ensures reliability and decoupling for message processing.

+ **AWS CDK (Cloud Development Kit)**: Deploys the entire infrastructure as code (IaC) using Python.