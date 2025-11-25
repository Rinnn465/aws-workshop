---
title: "Worklog Tuần 2"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---



### Mục tiêu tuần 2:

* Hiểu sâu về **Amazon VPC (Virtual Private Cloud)**: CIDR, Subnet, Route Table, ENI, Elastic IP, VPC Endpoint, Internet Gateway.
* Nắm vững kiến thức về **bảo mật mạng trên AWS**: Security Group (stateful), Network ACL (stateless), VPC Flow Logs.
* Hiểu và thực hành các mô hình **kết nối VPC**: VPC Peering, Transit Gateway và các hạn chế của từng phương pháp.
* Tìm hiểu về **kết nối Hybrid**: VPN Site-to-Site, VPN Client-to-Site, AWS Direct Connect.
* Nắm rõ các loại **Elastic Load Balancing (ELB)**: Application Load Balancer (ALB), Network Load Balancer (NLB), Classic Load Balancer (CLB), Gateway Load Balancer (GLB) và use case của từng loại.
* Thực hành các bài Lab về VPC và VPN Site-to-Site.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học lý thuyết về **Amazon VPC**: <br>&emsp; + VPC trong Region, CIDR IPv4/IPv6, giới hạn 5 VPC/Region <br>&emsp; + Subnet trong Availability Zone, Route Table (Default vs Custom) <br>&emsp; + Elastic Network Interface (ENI), Elastic IP (EIP) <br>&emsp; + VPC Endpoint (Interface Endpoint vs Gateway Endpoint) <br>&emsp; + Internet Gateway (IGW) - scale out tự động | 15/09/2025   | 15/09/2025      | [AWS Study Group - Module 2](https://www.youtube.com/watch?v=O9Ac_vGHquM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=25) |
| 3   | - Học về **bảo mật mạng**: <br>&emsp; + Security Group (stateful, chỉ allow rules, áp dụng trên ENI) <br>&emsp; + Network ACL (stateless, có allow/deny rules, áp dụng trên Subnet) <br>&emsp; + VPC Flow Logs (xuất sang CloudWatch/S3) <br> - Học về **VPC Peering**: kết nối 1:1, không hỗ trợ transitive routing, không hỗ trợ overlap IP <br> - Học về **Transit Gateway**: hub trung tâm, Transit Gateway Attachment ở AZ-level | 16/09/2025   | 16/09/2025      | [AWS Study Group - Module 2](https://www.youtube.com/watch?v=BPuD1l2hEQ4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=26) |
| 4   | - Học về **VPN**: <br>&emsp; + VPN Site-to-Site (Virtual Private Gateway + Customer Gateway) <br>&emsp; + VPN Client-to-Site <br> - Học về **AWS Direct Connect**: độ trễ 20-30ms, Hosted Connections vs Dedicated Connections <br> - Học chi tiết về **Elastic Load Balancing**: <br>&emsp; + Health check, Sticky session, Access logs <br>&emsp; + ALB (Layer 7, HTTP/HTTPS, path-based routing) <br>&emsp; + NLB (Layer 4, TCP/TLS, IP tĩnh, hiệu năng cao) <br>&emsp; + CLB (Layer 4+7, chi phí cao, ít tính năng) <br>&emsp; + GLB (cho Security appliances) | 17/09/2025   | 17/09/2025      | [AWS Study Group - Module 2](https://www.youtube.com/watch?v=CXU8D3kyxIc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=27) |
| 5   | - Thực hành **Lab03** - Amazon VPC và VPN Site-to-Site (18 bài lab): <br>&emsp; + Lab 03-1: Introduction, Subnets, Route Table, IGW, NAT Gateway <br>&emsp; + Lab 03-2: Security Group, Network ACLs, VPC Resource Map <br>&emsp; + Lab 03-3: Create VPC, Subnet, IGW, Route Table, Security Groups <br>&emsp; + Lab 03-4: Create EC2 Instances, Test connection, NAT Gateway, EC2 Instance Connect Endpoint | 18/09/2025   | 18/09/2025      | [Lab03 - VPC](https://www.youtube.com/watch?v=O5CIvG0Wt78&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=28) |


### Kết quả đạt được tuần 2:

* **Kiến thức về Amazon VPC**
  * Hiểu VPC (CIDR IPv4/IPv6, giới hạn 5 VPC/Region), Subnet (theo AZ), Route Table (Default vs Custom).
  * Nắm được ENI (card mạng ảo), EIP (IPv4 public tĩnh, charge phí khi không dùng).
  * Phân biệt VPC Endpoint: Interface Endpoint (ENI + IP Private) và Gateway Endpoint (Route Table, chỉ S3/DynamoDB).
  * Hiểu Internet Gateway (IGW) - scale out tự động.

* **Kiến thức về bảo mật mạng**
  * Phân biệt Security Group (stateful, chỉ allow, áp dụng trên ENI) và Network ACL (stateless, allow/deny, áp dụng trên Subnet).
  * Hiểu VPC Flow Logs (xuất sang CloudWatch/S3, không capture nội dung gói tin).

* **Kiến thức về kết nối VPC và Hybrid**
  * VPC Peering (kết nối 1:1, không transitive routing, không overlap IP).
  * Transit Gateway (hub trung tâm, Transit Gateway Attachment ở AZ-level).
  * VPN Site-to-Site (Virtual Private Gateway + Customer Gateway), VPN Client-to-Site.
  * AWS Direct Connect (độ trễ 20-30ms, Hosted/Dedicated Connections).

* **Kiến thức về Elastic Load Balancing**
  * Hiểu 4 loại ELB: ALB (Layer 7, HTTP/HTTPS, path-based routing), NLB (Layer 4, TCP/TLS, IP tĩnh, hiệu năng cao), CLB (Layer 4+7, ít dùng), GLB (Security appliances).
  * Nắm được health check, sticky session, access logs.

* **Kỹ năng thực hành**
  * Hoàn thành Lab03 (18 bài): tạo VPC, Subnet, IGW, NAT Gateway, Security Group, NACL, EC2 Instances, Route Table, test connection.
  * Nắm quy trình thiết lập VPC hoàn chỉnh và cấu hình kết nối giữa các subnet.

---

 Sau tuần 2, đã có nền tảng vững về Networking trên AWS (VPC, Security, Routing), các mô hình kết nối (Peering, Transit Gateway, VPN, Direct Connect), Load Balancing (ALB, NLB, CLB, GLB) và thực hành 18 bài Lab về VPC.


