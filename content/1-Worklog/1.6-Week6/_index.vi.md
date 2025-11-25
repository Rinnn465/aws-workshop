---
title: "Worklog Tuần 6"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Mục tiêu tuần 6:

* Hiểu rõ **kiến thức nền tảng về Database Concepts** bao gồm các khái niệm cơ bản như Database, Session, Primary Key, Foreign Key, Index, Partition, Execution Plan, Database Log, Buffer.
* Phân biệt rõ sự khác nhau giữa **RDBMS và NoSQL**, cũng như giữa **OLTP và OLAP**.
* Nắm vững các dịch vụ **AWS Database** chính:
  * **Amazon RDS** - Dịch vụ cơ sở dữ liệu quan hệ được quản lý
  * **Amazon Aurora** - RDBMS tối ưu với hiệu năng cao và storage layer cải tiến
  * **Amazon Redshift** - Data Warehouse cho OLAP workload với kiến trúc MPP
  * **Amazon ElastiCache** - Dịch vụ caching với Redis/Memcached
* Thực hành triển khai và quản lý **Amazon RDS** qua các bài lab chi tiết từ VPC setup đến backup/restore.
* Thực hành **Database Migration** với AWS Database Migration Service (DMS) và Schema Conversion Tool (SCT).
* Nghiên cứu các kiến trúc **RAG Chatbot và AI Agents** trên AWS để chuẩn bị cho dự án thực tế.


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu **Database Concepts**: <br>&emsp; + Database, Session, Primary Key, Foreign Key <br>&emsp; + Index, Partition, Execution Plan, Database Log, Buffer <br> - Phân biệt **RDBMS vs NoSQL**: <br>&emsp; + Schema cố định vs động <br>&emsp; + SQL vs collection-based query <br>&emsp; + Vertical scaling vs Horizontal scaling <br>&emsp; + Normalization vs Denormalization <br>&emsp; + Transaction Model: ACID vs BASE <br> - Hiểu rõ **OLTP vs OLAP**: <br>&emsp; + OLTP: Xử lý giao dịch nhanh, cập nhật thường xuyên, trọng tâm là data integrity <br>&emsp; + OLAP: Phân tích dữ liệu lịch sử, truy vấn phức tạp, trọng tâm là query performance | 13/10/2025   | 13/10/2025      | [AWS Study Group - Database Concepts](https://www.youtube.com/watch?v=OOD2RwWuLRw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=217) |
| 3   | - Nghiên cứu **Amazon RDS**: <br>&emsp; + Các engine hỗ trợ: Aurora, MySQL, PostgreSQL, MSSQL, Oracle, MariaDB <br>&emsp; + Tự động backup (cả log và database – tối đa 35 ngày) <br>&emsp; + Read Replica để phân tải read workload (reporting) <br>&emsp; + Multi-AZ (Primary/Standby) với auto failover <br>&emsp; + Mã hóa dữ liệu at rest và in transit <br>&emsp; + Storage Auto Scaling <br>&emsp; + Security Group và NACL protection <br> - Tìm hiểu **Amazon Aurora**: <br>&emsp; + Tối ưu storage layer, hiệu năng cao hơn RDS thông thường <br>&emsp; + Hỗ trợ MySQL và PostgreSQL compatible <br>&emsp; + **Back Track**: phục hồi DB về thời điểm trước đó <br>&emsp; + **Clone**: tạo bản sao nhanh chóng <br>&emsp; + **Global Database**: 1 Master + Multi Read ở các Region khác nhau <br>&emsp; + **Multi Master**: Multi Master database | 14/10/2025   | 14/10/2025      | [Amazon RDS Documentation](https://docs.aws.amazon.com/rds/) <br> [Amazon Aurora Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/) |
| 4   | - Nghiên cứu **Amazon Redshift**: <br>&emsp; + Data Warehouse được quản lý bởi AWS, dùng cho OLAP workload <br>&emsp; + Kiến trúc **MPP (Massively Parallel Processing)** Database <br>&emsp; + **Leader Node**: điều phối và tối ưu hóa truy vấn <br>&emsp; + **Compute Node**: lưu trữ và xử lý dữ liệu (compute + storage) <br>&emsp; + **Columnar Storage**: tối ưu cho phân tích và aggregation <br>&emsp; + Lõi PostgreSQL nhưng tối ưu cho OLAP <br>&emsp; + **Redshift Spectrum**: query data trực tiếp từ S3 <br>&emsp; + **Transient Cluster**: tối ưu chi phí <br> - Tìm hiểu **Amazon ElastiCache**: <br>&emsp; + Dịch vụ quản lý caching engines: Redis và Memcached <br>&emsp; + Tự động phát hiện và thay thế node failed <br>&emsp; + Đặt trước DB layer để cache dữ liệu, giảm tải cho DB <br>&emsp; + Ưu tiên **Redis** cho workload mới (tính năng đa dạng, hiệu năng tốt) <br>&emsp; + Yêu cầu viết và quản lý caching logic trên application | 14/10/2025   | 14/10/2025      | [Amazon Redshift Documentation](https://docs.aws.amazon.com/redshift/) <br> [Amazon ElastiCache Documentation](https://docs.aws.amazon.com/elasticache/) |
| 5   | - Thực hành **Lab 5 - Amazon RDS** (chi tiết từng bước): <br>&emsp; + **Lab05-2.1**: Create VPC <br>&emsp; + **Lab05-2.2**: Create EC2 Security Groups <br>&emsp; + **Lab05-2.3**: Create RDS Security Groups <br>&emsp; + **Lab05-2.4**: Create DB Subnet Group <br>&emsp; + **Lab05-3**: Create EC2 Instance <br>&emsp; + **Lab05-4**: Create RDS Database Instance <br>&emsp; + **Lab05-5**: Application Deployment <br>&emsp; + **Lab05-6**: Backup and Restore <br>&emsp; + **Lab05-7**: Cleanup Resources ✅ | 15/10/2025   | 15/10/2025      | [AWS Hands-on Labs - RDS](https://cloudjourney.awsstudygroup.com/) |
| 6   | - Thực hành **Lab 43 - Database Migration (DMS & SCT)** (17 sub-labs): <br>&emsp; + **Lab43-01**: EC2 Connect RDP Client <br>&emsp; + **Lab43-02**: EC2 Connect Fleet Manager <br>&emsp; + **Lab43-03**: SQL Server Source Config <br>&emsp; + **Lab43-04**: Oracle Connect Source DB <br>&emsp; + **Lab43-05**: Oracle Config Source DB <br>&emsp; + **Lab43-06**: Drop Constraint <br>&emsp; + **Lab43-07**: MSSQL to Aurora MySQL Target Config <br>&emsp; + **Lab43-08**: MSSQL to Aurora MySQL Create Project <br>&emsp; + **Lab43-09**: MSSQL to Aurora MySQL Schema Conversion <br>&emsp; + **Lab43-10**: Oracle to MySQL Schema Conversion <br>&emsp; + **Lab43-11**: Create Migration Task & Endpoint <br>&emsp; + **Lab43-12**: Inspect S3 <br>&emsp; + **Lab43-13**: Create Serverless Migration <br>&emsp; + **Lab43-14**: Create Event Notification <br>&emsp; + **Lab43-15**: Logs <br>&emsp; + **Lab43-16**: Troubleshoot Test Scenario - Memory Pressure <br>&emsp; + **Lab43-17**: Troubleshoot Test Scenario - Table Error <br> - Đọc blog và nghiên cứu kiến trúc: <br>&emsp; + **RAG Chatbot** trên AWS <br>&emsp; + **Advanced Multimodal Chatbot with Speech-to-Speech** <br> - **Họp nhóm** lên ý tưởng **pre-architecture cho dự án** | 17-18/10/2025   | 17-18/10/2025      | [RAG Chatbot on AWS](https://aws.amazon.com/vi/solutions/guidance/conversational-chatbots-using-retrieval-augmented-generation-on-aws/) <br> [Multimodal Chatbot with Speech-to-Speech](https://aws.amazon.com/vi/solutions/guidance/advanced-multimodal-chatbot-with-speech-to-speech-on-aws/) |


### Kết quả đạt được tuần 6:

* Hiểu rõ **Database Concepts cơ bản**:
  * Các khái niệm: Session, Primary/Foreign Key, Index, Partition, Execution Plan, Buffer, Database Log
  * So sánh **RDBMS vs NoSQL**: Schema (cố định vs động), Scaling (vertical vs horizontal), Transaction (ACID vs BASE)
  * Phân biệt **OLTP vs OLAP**: Transaction processing vs Analytical processing

* Nắm vững **AWS Database Services**:
  * **Amazon RDS**: 6 engines, auto backup (35 ngày), Read Replica, Multi-AZ failover, encryption, auto scaling
  * **Amazon Aurora**: Back Track, Clone, Global Database, Multi Master - hiệu năng vượt trội
  * **Amazon Redshift**: MPP architecture, Columnar Storage, Redshift Spectrum - tối ưu cho OLAP
  * **Amazon ElastiCache**: Redis/Memcached, auto node replacement, giảm tải database

* Hoàn thành **Lab thực hành**:
  * ✅ **Lab 5 - Amazon RDS**: Triển khai end-to-end từ VPC, Security Groups, RDS instance, application deployment đến backup/restore (7 sub-labs)
  * ✅ **Lab 43 - Database Migration**: DMS & SCT, migrate MSSQL/Oracle sang Aurora MySQL, troubleshooting (17 sub-labs)

* Nghiên cứu **kiến trúc RAG Chatbot và AI Agents** trên AWS, họp nhóm lên ý tưởng pre-architecture cho dự án.


