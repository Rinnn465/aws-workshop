---
title: "Week 6 Worklog"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Week 6 Objectives:

* Clearly understand **foundational Database Concepts** including basic concepts such as Database, Session, Primary Key, Foreign Key, Index, Partition, Execution Plan, Database Log, Buffer.
* Clearly differentiate between **RDBMS and NoSQL**, as well as between **OLTP and OLAP**.
* Master main **AWS Database** services:
  * **Amazon RDS** - Managed relational database service
  * **Amazon Aurora** - Optimized RDBMS with high performance and improved storage layer
  * **Amazon Redshift** - Data Warehouse for OLAP workload with MPP architecture
  * **Amazon ElastiCache** - Caching service with Redis/Memcached
* Practice deploying and managing **Amazon RDS** through detailed labs from VPC setup to backup/restore.
* Practice **Database Migration** with AWS Database Migration Service (DMS) and Schema Conversion Tool (SCT).
* Research **RAG Chatbot and AI Agents** architectures on AWS to prepare for real projects.


### Tasks to carry out this week:
| Day | Tasks                                                                                                                                                                                   | Start date | Completion date | References                            |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------- |
| 2   | - Learn **Database Concepts**: <br>&emsp; + Database, Session, Primary Key, Foreign Key <br>&emsp; + Index, Partition, Execution Plan, Database Log, Buffer <br> - Differentiate **RDBMS vs NoSQL**: <br>&emsp; + Fixed vs dynamic schema <br>&emsp; + SQL vs collection-based query <br>&emsp; + Vertical scaling vs Horizontal scaling <br>&emsp; + Normalization vs Denormalization <br>&emsp; + Transaction Model: ACID vs BASE <br> - Clearly understand **OLTP vs OLAP**: <br>&emsp; + OLTP: Fast transaction processing, frequent updates, focus on data integrity <br>&emsp; + OLAP: Historical data analysis, complex queries, focus on query performance | 13/10/2025   | 13/10/2025      | [AWS Study Group - Database Concepts](https://www.youtube.com/watch?v=OOD2RwWuLRw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=217) |
| 3   | - Research **Amazon RDS**: <br>&emsp; + Supported engines: Aurora, MySQL, PostgreSQL, MSSQL, Oracle, MariaDB <br>&emsp; + Auto backup (both log and database – max 35 days) <br>&emsp; + Read Replica to offload read workload (reporting) <br>&emsp; + Multi-AZ (Primary/Standby) with auto failover <br>&emsp; + Data encryption at rest and in transit <br>&emsp; + Storage Auto Scaling <br>&emsp; + Security Group and NACL protection <br> - Learn **Amazon Aurora**: <br>&emsp; + Optimized storage layer, higher performance than regular RDS <br>&emsp; + Supports MySQL and PostgreSQL compatible <br>&emsp; + **Back Track**: restore DB to previous point in time <br>&emsp; + **Clone**: fast copy creation <br>&emsp; + **Global Database**: 1 Master + Multi Read in different Regions <br>&emsp; + **Multi Master**: Multi Master database | 14/10/2025   | 14/10/2025      | [Amazon RDS Documentation](https://docs.aws.amazon.com/rds/) <br> [Amazon Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/) |
| 4   | - Research **Amazon Redshift**: <br>&emsp; + Data Warehouse managed by AWS, used for OLAP workload <br>&emsp; + **MPP (Massively Parallel Processing)** Database architecture <br>&emsp; + **Leader Node**: coordinate and optimize queries <br>&emsp; + **Compute Node**: store and process data (compute + storage) <br>&emsp; + **Columnar Storage**: optimized for analytics and aggregation <br>&emsp; + PostgreSQL core but optimized for OLAP <br>&emsp; + **Redshift Spectrum**: query data directly from S3 <br>&emsp; + **Transient Cluster**: cost optimization <br> - Learn **Amazon ElastiCache**: <br>&emsp; + Manage caching engines: Redis and Memcached <br>&emsp; + Auto detect and replace failed nodes <br>&emsp; + Place before DB layer to cache data, reduce DB load <br>&emsp; + Prioritize **Redis** for new workloads (diverse features, good performance) <br>&emsp; + Require writing and managing caching logic on application | 14/10/2025   | 14/10/2025      | [Amazon Redshift Documentation](https://docs.aws.amazon.com/redshift/) <br> [Amazon ElastiCache Documentation](https://docs.aws.amazon.com/elasticache/) |
| 5   | - Practice **Lab 5 - Amazon RDS** (detailed step by step): <br>&emsp; + **Lab05-2.1**: Create VPC <br>&emsp; + **Lab05-2.2**: Create EC2 Security Groups <br>&emsp; + **Lab05-2.3**: Create RDS Security Groups <br>&emsp; + **Lab05-2.4**: Create DB Subnet Group <br>&emsp; + **Lab05-3**: Create EC2 Instance <br>&emsp; + **Lab05-4**: Create RDS Database Instance <br>&emsp; + **Lab05-5**: Application Deployment <br>&emsp; + **Lab05-6**: Backup and Restore <br>&emsp; + **Lab05-7**: Cleanup Resources ✅ | 15/10/2025   | 15/10/2025      | [AWS Hands-on Labs - RDS](https://cloudjourney.awsstudygroup.com/) |
| 6   | - Practice **Lab 43 - Database Migration (DMS & SCT)** (17 sub-labs): <br>&emsp; + **Lab43-01**: EC2 Connect RDP Client <br>&emsp; + **Lab43-02**: EC2 Connect Fleet Manager <br>&emsp; + **Lab43-03**: SQL Server Source Config <br>&emsp; + **Lab43-04**: Oracle Connect Source DB <br>&emsp; + **Lab43-05**: Oracle Config Source DB <br>&emsp; + **Lab43-06**: Drop Constraint <br>&emsp; + **Lab43-07**: MSSQL to Aurora MySQL Target Config <br>&emsp; + **Lab43-08**: MSSQL to Aurora MySQL Create Project <br>&emsp; + **Lab43-09**: MSSQL to Aurora MySQL Schema Conversion <br>&emsp; + **Lab43-10**: Oracle to MySQL Schema Conversion <br>&emsp; + **Lab43-11**: Create Migration Task & Endpoint <br>&emsp; + **Lab43-12**: Inspect S3 <br>&emsp; + **Lab43-13**: Create Serverless Migration <br>&emsp; + **Lab43-14**: Create Event Notification <br>&emsp; + **Lab43-15**: Logs <br>&emsp; + **Lab43-16**: Troubleshoot Test Scenario - Memory Pressure <br>&emsp; + **Lab43-17**: Troubleshoot Test Scenario - Table Error <br> - Read blogs and research architecture: <br>&emsp; + **RAG Chatbot** on AWS <br>&emsp; + **Advanced Multimodal Chatbot with Speech-to-Speech** <br> - **Team meeting** to brainstorm **pre-architecture for project** | 17-18/10/2025   | 17-18/10/2025      | [RAG Chatbot on AWS](https://aws.amazon.com/vi/solutions/guidance/conversational-chatbots-using-retrieval-augmented-generation-on-aws/) <br> [Multimodal Chatbot with Speech-to-Speech](https://aws.amazon.com/vi/solutions/guidance/advanced-multimodal-chatbot-with-speech-to-speech-on-aws/) |


### Week 6 Achievements:

* Clearly understand **basic Database Concepts**:
  * Concepts: Session, Primary/Foreign Key, Index, Partition, Execution Plan, Buffer, Database Log
  * Compare **RDBMS vs NoSQL**: Schema (fixed vs dynamic), Scaling (vertical vs horizontal), Transaction (ACID vs BASE)
  * Differentiate **OLTP vs OLAP**: Transaction processing vs Analytical processing

* Master **AWS Database Services**:
  * **Amazon RDS**: 6 engines, auto backup (35 days), Read Replica, Multi-AZ failover, encryption, auto scaling
  * **Amazon Aurora**: Back Track, Clone, Global Database, Multi Master - superior performance
  * **Amazon Redshift**: MPP architecture, Columnar Storage, Redshift Spectrum - optimized for OLAP
  * **Amazon ElastiCache**: Redis/Memcached, auto node replacement, reduce database load

* Completed **hands-on Labs**:
  * ✅ **Lab 5 - Amazon RDS**: End-to-end deployment from VPC, Security Groups, RDS instance, application deployment to backup/restore (7 sub-labs)
  * ✅ **Lab 43 - Database Migration**: DMS & SCT, migrate MSSQL/Oracle to Aurora MySQL, troubleshooting (17 sub-labs)

* Researched **RAG Chatbot and AI Agents architecture** on AWS, team meeting to brainstorm pre-architecture for project.
