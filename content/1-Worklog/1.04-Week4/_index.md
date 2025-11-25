---
title: "Week 4 Worklog"
date: "2025-09-09"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---



### Week 4 Objectives:

* Deeply understand **Virtual Machine, Compute & Storage Management** in AWS system:
  * Master how services like **EC2**, **Amazon Lightsail**, **AWS EFS/FSX**, **AWS Application Migration Services (MGN)**, **Amazon Simple Storage (S3)** work.

* **Operating Virtual Machine & Storage:** Proficient in deploying and managing flexible computing resources (EC2) and simplified solutions (Amazon Lightsail).

* **Deploy file and object storage:** Effectively use managed file storage services (AWS EFS/FSX) and durable, highly scalable object storage service (Amazon Simple Storage (S3)).

* **Migrate servers to Cloud:** Master the process and tools for migrating applications/servers from On-premises environment to AWS using AWS Application Migration Services (MGN).

* **Expand knowledge:** Develop skills in reading and accurately translating AWS technical documentation to synthesize in-depth knowledge and support high-quality information sharing within the team.

### Tasks to carry out this week:
| Day | Tasks                                                                                                                                                                                   | Start date | Completion date | References                            |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------- |
| 2   | - Research **Compute & Storage** services in AWS: <br> &emsp; + **Amazon EC2 (Elastic Compute Cloud):** Learn instance types, configure security groups, and manage EC2 lifecycle.<br> &emsp;&emsp;• Research **Instance Types** (General Purpose, Compute Optimized, Memory Optimized) and **Pricing Models** (On-Demand, Reserved, Spot).<br><br> &emsp; + **Amazon Lightsail:** Deploy simplified virtual private server, compare with EC2 regarding use cases and pricing.<br><br> &emsp; + **Amazon S3 (Simple Storage Service):** Manage buckets, object storage, versioning, lifecycle policies and storage classes (Standard, IA, Glacier).<br><br> &emsp; + **AWS EFS/FSX:** Learn managed file storage, differentiate between EFS (Linux) and FSx (Windows/Lustre), configure mount points. | 29/09/2025 | 29/09/2025 | |
| 3   | - **Deploy & manage EC2 Instance with best practices:** <br> &emsp; + Configure User Data to automatically initialize instance on launch. <br> &emsp; + Set up Elastic IP and Network Interface for EC2. <br> &emsp; + Use EC2 Instance Connect and Session Manager for secure access. <br><br> - **Optimize storage with Amazon S3:** <br> &emsp; + Configure S3 Bucket Policies and Access Control Lists (ACL). <br> &emsp; + Set up S3 Lifecycle Rules to automatically transition storage classes. <br> &emsp; + Practice S3: initialize S3 Bucket, Set up Notification, Create Back up plan, Test Restore. <br><br> - **Compare EC2 and Lightsail:** <br> &emsp; + Analyze pros and cons between the two services. <br> &emsp; + Identify suitable use cases for each service (startup vs enterprise). <br> &emsp; + Evaluate costs and management complexity. | 30/09/2025   | 30/09/2025      | |
| 4   | - **Learn AWS EFS and FSx:** <br> &emsp; + Research architecture and how Elastic File System (EFS) works. <br> &emsp; + Learn performance modes (General Purpose, Max I/O) and throughput modes. <br> &emsp; + Compare FSx for Windows File Server and FSx for Lustre. <br><br> - **Explore AWS Application Migration Service (MGN):** <br> &emsp; + Learn migration process from on-premises to AWS Cloud. <br> &emsp; + Differentiate between MGN and other migration methods (SMS, CloudEndure). | 02/10/2025   | 2/10/2025      | |
| 5   | - Translate blogs & documents: <br> &emsp; + Translate content from document 1: Data Protection and Security Best Practices with Veeam on AWS <br> &emsp; + Translate content from document 2: Dynamic text-to-SQL for enterprise workloads with Amazon Bedrock Agents <br> &emsp; + Translate content from document 3: Effectively implementing resource control policies in a multi-account environment | 03/10/2025   | 03/10/2025      | [Google Doc 1](https://docs.google.com/document/d/1eH7LHqCWXmIKiNL2tUvtiEWIToT1TC9x0WNHfBJpwcQ/edit?usp=sharing), [Google Doc 2](https://docs.google.com/document/d/1Yn6shC-ugPCWvHEYEJNMrnMWqhtEQziNnAKIcY24XVU/edit?usp=sharing), [Google Doc 3](https://docs.google.com/document/d/1U9-3HcugvzAzNkP9gHq-rSV-UyjwWMjzI5xVKyIxgXc/edit?usp=sharing) |


### Week 4 Achievements:

* Completed learning and practicing **Compute & Storage services in AWS**, including:
  * **Amazon EC2** – Mastered instance types, pricing models, and virtual machine lifecycle management.
  * **Amazon Lightsail** – Deploy and manage simplified VPS for small applications.
  * **Amazon S3** – Manage object storage with versioning, lifecycle policies and storage classes.
  * **AWS EFS/FSx** – Deploy and configure managed file storage for Linux (EFS) and Windows/HPC (FSx).
  * **AWS Application Migration Service (MGN)** – Understand server migration process from on-premises to AWS Cloud.

* Completed **Compute & Storage hands-on labs**:
  * Initialize and manage EC2 Instance 
  * EC2 Auto Scaling & Load Balancing 
  * Amazon Lightsail Setup 
  * S3 Bucket Management & Lifecycle Policies 
  * EFS File System Configuration 
  * S3 Versioning & Cross-Region Replication 

* Mastered important concepts:
  * **EC2 Instance Types** and **Pricing Models** (On-Demand, Reserved, Spot).
  * **S3 Storage Classes** and how to optimize storage costs.
  * **Performance modes** and **Throughput modes** of EFS.
  * **Migration process** with AWS MGN.

* Know how to **compare and choose suitable services**:
  * Differentiate between EC2 and Lightsail based on use case and complexity.
  * Understand when to use EFS (Linux workloads) vs FSx (Windows/HPC workloads).

* Proficient in **best practices** for EC2 and S3:
  * Configure User Data, Elastic IP, Security Groups for EC2.
  * Set up S3 Bucket Policies, ACL, and Lifecycle Rules.
  * Use EC2 Instance Connect and Session Manager for secure access.
