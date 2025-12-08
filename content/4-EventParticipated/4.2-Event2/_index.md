---
title: "Event 2"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Event Takeaways: "AWS Cloud Mastery Series #2 – DevOps on AWS"

### Program Goals

- Explore Infrastructure as Code (IaC) concepts alongside supporting toolchains.
- Guide participants through CI/CD pipeline construction and AWS DevOps services overview.
- Demonstrate effective monitoring and observability implementation with native AWS services.
- Present comprehensive overview of container workloads and deployment models on AWS.

### Speakers

- **Truong Quang Tinh** – AWS Community Builder, Platform Engineer (TymeX)  
- **Bao Huynh** – AWS Community Builder  
- **Nguyen Khanh Phuc Thinh** – AWS Community Builder  
- **Tran Dai Vi** – AWS Community Builder  
- **Huynh Hoang Long** – AWS Community Builder  
- **Pham Hoang Quy** – AWS Community Builder  
- **Nghiem Le** – AWS Community Builder  
- **Dinh Le Hoang Anh** – Cloud Engineer Trainee, First Cloud AI Journey

### Key Highlights

### **1. Building a DevOps Foundation**

The speakers highlighted that DevOps is less about job titles and more about adopting habits that improve delivery:  
- Automating repetitive tasks  
- Sharing knowledge across roles  
- Continuously experimenting and learning  
- Tracking measurable outcomes instead of relying on assumptions  

They also shared common pitfalls that early DevOps learners face, such as relying too much on tutorials without building real projects or comparing progress with others instead of focusing on steady improvement.

---

### **2. Infrastructure as Code in Practice**

Rather than sticking to one tool, the speakers compared several IaC approaches:

- **CloudFormation** as AWS’s native template engine  
- **CDK** for developers who prefer writing infrastructure using programming languages  
- **Terraform** for teams working across multiple cloud providers  

The differences between Stacks, Constructs, State files, and abstraction layers were explained using practical examples.

A strong message from this section: infrastructure rebuilt using IaC tends to be *more consistent and maintainable* than anything configured manually.

---

### **3. Containers and Deployment Models**

The container portion took a step-by-step approach, starting with what a Dockerfile represents and how images are created.  
From there, the talk expanded into AWS services:

- **ECR** for storing and scanning container images  
- **ECS & EKS** for orchestration  
- **App Runner** for teams who want to deploy without dealing with cluster management  

The comparison between ECS and EKS helped clarify when each should be used.

---

### **4. Monitoring and Tracing**

The final portion of the event covered AWS CloudWatch and X-Ray:

- CloudWatch as the central source for metrics, dashboards, alarms, and logs  
- X-Ray for visualizing request flows and identifying latency bottlenecks  

The speakers stressed that observability is not something added at the end—it must be integrated into the architecture from the beginning.

---
### Learning Outcomes
- Monitoring and observability require integration from initial architecture phases, not as afterthoughts, to guarantee system stability and rapid incident response.
- Comprehending distinctions among AWS container services (ECR, ECS, EKS, App Runner) enables optimal solution selection for specific scenarios.
- IaC tooling decisions (CloudFormation, CDK, Terraform) should align with team capabilities and project constraints.
- Infrastructure as Code (IaC) provides superior infrastructure consistency and maintainability versus manual configuration approaches.
- Automation, knowledge distribution, continuous experimentation, and outcome measurement form essential pillars for DevOps achievement.
- DevOps transcends job titles—it embodies a mindset and habit framework for enhancing software delivery.


### Real-World Application

#### Scenario: AI Chatbot Development on AWS

Post-workshop knowledge will be applied to an AI Chatbot project when opportunities arise. Implementation strategy includes:

- **Infrastructure as Code Strategy:** Utilize AWS CDK to codify complete infrastructure stack (Lambda functions, API Gateway endpoints, DynamoDB tables, S3 buckets, IAM roles, etc.), facilitating straightforward reusability and consistent scaling.
- **CI/CD Pipeline Implementation:** Deploy AWS CodePipeline to automate build, testing, and production deployment workflows, guaranteeing all code modifications undergo automated testing and deployment.

Through DevOps methodologies and AWS service integration, the AI chatbot project can achieve accelerated development, continuous deployment capabilities, and maintain effortless scalability when required.


### Workshop Impressions
- The workshop delivered practical insights into modern organizational approaches to DevOps implementation on AWS.
Speakers blended theoretical frameworks with extensive real-world case studies, illuminating tools such as CloudFormation, CDK, Terraform, plus container operations and deployment methodologies on AWS.

- The event provided excellent networking opportunities with peers sharing similar interests and absorbing practical wisdom from experienced practitioners.
#### Event photography
![Event 2-1](/images/4-EventParticipated/event2-1.jpg)
![Event 2-2](/images/4-EventParticipated/event2-2.jpg)
![Event 2-3](/images/4-EventParticipated/event2-3.jpg)
