---
title: "Worklog Tuần 4"
date: "2025-09-09"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---



### Mục tiêu tuần 4:

* Hiểu sâu về **Virtual Machine, Compute & Storage Management** trong hệ thống AWS:
  * Nắm được cách hoạt động của các dịch vụ như **EC2**, **Amazon Lightsail**, **AWS EFS/FSX** **AWS Application Migration Services (MGN)**, **Amazon Simple Storage (S3)**.

* **Vận hành Virtual Machine & Lưu trữ:** Thành thạo việc triển khai và quản lý các tài nguyên điện toán linh hoạt (EC2) và đơn giản hóa (Amazon Lightsail).

* **Triển khai lưu trữ tệp và đối tượng:** Sử dụng hiệu quả các dịch vụ lưu trữ tệp được quản lý (AWS EFS/FSX) và dịch vụ lưu trữ đối tượng bền bỉ, có khả năng mở rộng cao (Amazon Simple Storage (S3)).

* **Di chuyển máy chủ lên Cloud:** Nắm vững quy trình và công cụ di chuyển ứng dụng/máy chủ từ môi trường On-premises sang AWS bằng AWS Application Migration Services (MGN).

* **Mở rộng thêm kiến thức:** Phát triển kỹ năng đọc hiểu và dịch chính xác tài liệu kỹ thuật AWS để tổng hợp kiến thức chuyên sâu và hỗ trợ chia sẻ thông tin chất lượng cao trong nội bộ đội nhóm.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu các dịch vụ **Compute & Storage** trong AWS: <br> &emsp; + **Amazon EC2 (Elastic Compute Cloud):** Tìm hiểu các loại instance, cấu hình security group, và quản lý lifecycle của EC2.<br> &emsp;&emsp;• Nghiên cứu **Instance Types** (General Purpose, Compute Optimized, Memory Optimized) và **Pricing Models** (On-Demand, Reserved, Spot).<br><br> &emsp; + **Amazon Lightsail:** Triển khai virtual private server đơn giản hóa, so sánh với EC2 về use case và pricing.<br><br> &emsp; + **Amazon S3 (Simple Storage Service):** Quản lý bucket, object storage, versioning, lifecycle policies và storage classes (Standard, IA, Glacier).<br><br> &emsp; + **AWS EFS/FSX:** Tìm hiểu file storage được quản lý, phân biệt giữa EFS (Linux) và FSx (Windows/Lustre), cấu hình mount points.<br><br>
| 3   | - **Triển khai & quản lý EC2 Instance với best practices:** <br> &emsp; + Cấu hình User Data để tự động khởi tạo instance khi launch. <br> &emsp; + Thiết lập Elastic IP và Network Interface cho EC2. <br> &emsp; + Sử dụng EC2 Instance Connect và Session Manager để truy cập an toàn. <br><br> - **Tối ưu hóa lưu trữ với Amazon S3:** <br> &emsp; + Cấu hình S3 Bucket Policies và Access Control Lists (ACL). <br> &emsp; + Thiết lập S3 Lifecycle Rules để tự động chuyển đổi storage class. <br> &emsp; + Thực hành S3 khởi tạo S3 Bucket, Set up Notification, Tạo Back up plan, Test Restore. <br><br> - **So sánh EC2 và Lightsail:** <br> &emsp; + Phân tích ưu nhược điểm giữa hai dịch vụ. <br> &emsp; + Xác định use case phù hợp cho mỗi dịch vụ (startup vs enterprise). <br> &emsp; + Đánh giá chi phí và độ phức tạp quản lý. | 29/09/2025   | 29/09/2025      |
| 4   | - **Tìm hiểu AWS EFS và FSx:** <br> &emsp; + Nghiên cứu kiến trúc và cách hoạt động của Elastic File System (EFS). <br> &emsp; + Tìm hiểu các chế độ performance (General Purpose, Max I/O) và throughput modes. <br> &emsp; + So sánh FSx for Windows File Server và FSx for Lustre. <br> &emsp; <br><br> - **Khám phá AWS Application Migration Service (MGN):** <br> &emsp; + Tìm hiểu quy trình migration từ on-premises lên AWS Cloud. <br> &emsp; <br> &emsp; + Phân biệt giữa MGN và các phương pháp migration khác (SMS, CloudEndure). | 30/9/2025   | 30/9/2025      |
| 5   | - Dịch blog & tài liệu: <br> &emsp; + Dịch nội dung từ document 1: Data Protection and Security Best Practices with Veeam on AWS <br> &emsp; + Dịch nội dung từ document 2: Dynamic text-to-SQL for enterprise workloads with Amazon Bedrock Agents <br> &emsp; + Dịch nội dung từ document 3: Effectively implementing resource control policies in a multi-account environment | 03/10/2025   | 03/10/2025      | 
[Google Doc 1](https://docs.google.com/document/d/1eH7LHqCWXmIKiNL2tUvtiEWIToT1TC9x0WNHfBJpwcQ/edit?usp=sharing) <br>[Google Doc 2](https://docs.google.com/document/d/1Yn6shC-ugPCWvHEYEJNMrnMWqhtEQziNnAKIcY24XVU/edit?usp=sharing) <br> [Google Doc 3](https://docs.google.com/document/d/1U9-3HcugvzAzNkP9gHq-rSV-UyjwWMjzI5xVKyIxgXc/edit?usp=sharing) |


### Kết quả đạt được tuần 4:

* Hoàn thành tìm hiểu và thực hành các **dịch vụ Compute & Storage trong AWS**, bao gồm:
  * **Amazon EC2** – Nắm vững các loại instance, pricing models, và quản lý lifecycle của virtual machine.
  * **Amazon Lightsail** – Triển khai và quản lý VPS đơn giản hóa cho các ứng dụng nhỏ.
  * **Amazon S3** – Quản lý object storage với versioning, lifecycle policies và các storage classes.
  * **AWS EFS/FSx** – Triển khai và cấu hình file storage được quản lý cho Linux (EFS) và Windows/HPC (FSx).
  * **AWS Application Migration Service (MGN)** – Hiểu quy trình migration máy chủ từ on-premises lên AWS Cloud.

* Hoàn thành các bài **lab thực hành Compute & Storage**:
  * Khởi tạo và quản lý EC2 Instance 
  * EC2 Auto Scaling & Load Balancing 
  * Amazon Lightsail Setup 
  * S3 Bucket Management & Lifecycle Policies 
  * EFS File System Configuration 
  * S3 Versioning & Cross-Region Replication 

* Nắm vững các khái niệm quan trọng:
  * **EC2 Instance Types** và **Pricing Models** (On-Demand, Reserved, Spot).
  * **S3 Storage Classes** và cách tối ưu chi phí lưu trữ.
  * **Performance modes** và **Throughput modes** của EFS.
  * **Quy trình Migration** với AWS MGN.

* Biết cách **so sánh và lựa chọn dịch vụ phù hợp**:
  * Phân biệt giữa EC2 và Lightsail dựa trên use case và complexity.
  * Hiểu khi nào nên sử dụng EFS (Linux workloads) vs FSx (Windows/HPC workloads).

* Thành thạo **best practices** cho EC2 và S3:
  * Cấu hình User Data, Elastic IP, Security Groups cho EC2.
  * Thiết lập S3 Bucket Policies, ACL, và Lifecycle Rules.
  * Sử dụng EC2 Instance Connect và Session Manager để truy cập an toàn.






