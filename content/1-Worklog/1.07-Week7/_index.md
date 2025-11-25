---
title: "Week 7 Worklog"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---


### Week 7 Objectives:

* Learn how to **draw and design AWS architecture** using draw.io following best practices.
* Continue developing and **refining pre-architecture** for chatbot project.
* Define **direction** for project, including main features and use cases.
* Research **Text-to-SQL** mechanism and how to apply LLM to convert natural language to SQL queries.
* Analyze **database security** issues when chatbot interacts directly with DB (permission limits, access control).
* **Review foundational AWS knowledge** to prepare for exam.

---

### Tasks to carry out this week:
| Day | Tasks | Start date | Completion date | References |
| --- | ---------- | ------------- | ---------------- | --------------- |
| 2 | - Learn how to **draw AWS architecture** through tutorial video: <br>&emsp; + Use draw.io with AWS icons <br>&emsp; + Best practices in designing architecture diagrams <br>&emsp; + How to show flow and connections between services <br> - Note incident: **AWS outage at us-east-1**, severely affecting many global systems | 20/10/2025 | 20/10/2025 | [AWS Study Group](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=2) |
| 3 | - Continue **drawing and editing architecture** for project: <br>&emsp; + Based on brainstormed pre-architecture <br>&emsp; + Add new components <br>&emsp; + Optimize flow and connections <br> - **Team meeting on project direction**: <br>&emsp; + Define main chatbot objectives <br>&emsp; + Define scope and features <br>&emsp; + Analyze use cases | 21/10/2025 | 21/10/2025 | [Notion - Pre Architecture](https://www.notion.so/pre-archi-28fd23b23efb808b978dfb3f9a20389d) <br> [Notion - Directions](https://www.notion.so/Directions-295d23b23efb80bb9500e5cb3222414c) |
| 4 | - Research **Text-to-SQL mechanism**: <br>&emsp; + Read paper: "HEXGEN-FLOW: Optimizing LLM Inference Request Scheduling for Agentic Text-to-SQL" <br>&emsp; + Understand how LLM converts natural language to SQL queries <br>&emsp; + Analyze processing flow and optimization techniques <br> - **Team meeting on chatbot interaction with database**: <br>&emsp; + Clarify how chatbot processes Text-to-SQL <br>&emsp; + Limit chatbot permissions (READ-ONLY vs READ-WRITE) <br>&emsp; + Secure sensitive information <br>&emsp; + Control dangerous commands (DROP, DELETE, UPDATE) | 22/10/2025 | 22/10/2025 | [Paper - HEXGEN-FLOW](https://arxiv.org/pdf/2505.05286) <br> Notion Meeting Notes |
| 5 | - **Review foundational AWS knowledge**: <br>&emsp; + Review learned services (EC2, RDS, S3, Lambda, etc.) <br>&emsp; + Review best practices and use cases <br>&emsp; + Prepare for periodic exam | 23/10/2025 | 23/10/2025 | [Cloud Journey - AWS Study Group](https://cloudjourney.awsstudygroup.com/) |

---

### Week 7 Achievements:

* Mastered how to **draw AWS architecture** using draw.io 

* **Improved pre-architecture** for chatbot project

* Clearly defined **direction and scope** for project:
  * Main chatbot objectives and features
  * Specific use cases
  * Initial deployment phase scope

* Deep understanding of **Text-to-SQL mechanism**:
  * How LLM converts natural language to SQL queries
  * Processing flow and optimization techniques from HEXGEN-FLOW paper
  * Challenges in parsing and generating accurate SQL

* Detailed analysis of **database security issues** when chatbot interacts with DB:
  * Determined need to limit chatbot permissions (READ-ONLY or allow WRITE)
  * How to control dangerous commands (invalid DROP, DELETE, UPDATE)
  * Protect sensitive information and prevent SQL injection
  * Design appropriate permission model

* Noted and tracked **AWS outage incident at us-east-1**
