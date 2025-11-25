---
title: "Worklog Tuần 3"
date: "2025-09-09"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---



### Mục tiêu tuần 3:

* Thực hành các bài Lab về **Route 53 Resolver** để thiết lập Hybrid DNS giữa AWS và on-premises.
* Thực hành **VPC Peering** để kết nối 2 VPC, cấu hình Security Group, NACL, Route Tables và Cross-Peer DNS.
* Thực hành **AWS Transit Gateway** để kết nối nhiều VPC qua một hub trung tâm, cấu hình Transit Gateway Attachments và Route Tables.
* Củng cố kiến thức về Networking trên AWS thông qua các bài Lab thực hành.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Thực hành **Lab10** - Hybrid DNS với Route 53 Resolver (11 bài lab): <br>&emsp; + Lab10-01: Introduction - Tìm hiểu về Hybrid DNS <br>&emsp; + Lab10-02.1: Generate Key Pair <br>&emsp; + Lab10-02.2: Initialize CloudFormation Template <br>&emsp; + Lab10-02.3: Configure Security Group <br>&emsp; + Lab10-03: Connect to RDGW (Remote Desktop Gateway) <br>&emsp; + Lab10-05: Set up DNS <br>&emsp; + Lab10-05.1: Create Route 53 Outbound Endpoint <br>&emsp; + Lab10-05.2: Create Route 53 Resolver Rules <br>&emsp; + Lab10-05.3: Create Route 53 Inbound Endpoints <br>&emsp; + Lab10-05.4: Test results <br>&emsp; + Lab10-06: Clean up resources | 22/09/2025   | 22/09/2025      | [Lab10 - Route 53 Resolver](https://www.youtube.com/watch?v=FGicpWOmMDI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=45) | (https://000010.awsstudygroup.com/) | 
| 3   | - Thực hành **Lab19** - VPC Peering (8 bài lab): <br>&emsp; + Lab19-1: Introduction - Set up VPC Peering <br>&emsp; + Lab19-2.1: Initialize CloudFormation Templates <br>&emsp; + Lab19-2.2: Create Security Group <br>&emsp; + Lab19-2.3: Create EC2 Instance <br>&emsp; + Lab19-3: Update Network ACL (NACLs) <br>&emsp; + Lab19-4: Create a Peering Connection <br>&emsp; + Lab19-5: Configure Route Tables <br>&emsp; + Lab19-6: Enable Cross-Peer DNS | 23/09/2025   | 23/09/2025     | [Lab19 - VPC Peering](https://www.youtube.com/watch?v=sllYqAECBoM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=56) | (https://000019.awsstudygroup.com/) |
| 4   | - Thực hành **Lab20** - AWS Transit Gateway (7 bài lab): <br>&emsp; + Lab20-1: Introduction - Set up AWS Transit Gateway <br>&emsp; + Lab20-2: Preparation steps <br>&emsp; + Lab20-3: Create Transit Gateway <br>&emsp; + Lab20-4: Create Transit Gateway Attachments <br>&emsp; + Lab20-5: Create Transit Gateway Route Tables <br>&emsp; + Lab20-6: Add Transit Gateway Routes to VPC Route Tables <br>&emsp; + Lab20-7: Clean up resources | 25/09/2025  | 25/09/2025     | [Lab20 - Transit Gateway](https://www.youtube.com/watch?v=ybLa49z7FFg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=65) |  (https://000020.awsstudygroup.com/) |


### Kết quả đạt được tuần 3:

* **Lab10 - Hybrid DNS với Route 53 Resolver (11 bài lab)**
  * Thiết lập Hybrid DNS để kết nối DNS giữa AWS VPC và on-premises data center.
  * Tạo và cấu hình **Route 53 Outbound Endpoint** để resolve domain name từ VPC sang on-premises.
  * Tạo và cấu hình **Route 53 Inbound Endpoint** để resolve domain name từ on-premises vào VPC.
  * Tạo **Route 53 Resolver Rules** để định tuyến DNS queries.
  * Sử dụng CloudFormation để khởi tạo infrastructure, cấu hình Security Group cho DNS traffic.
  * Connect tới Remote Desktop Gateway (RDGW) để quản lý môi trường Windows.
  * Test kết quả và verify DNS resolution hoạt động đúng giữa 2 môi trường.

* **Lab19 - VPC Peering (8 bài lab)**
  * Thiết lập **VPC Peering Connection** để kết nối 2 VPC với nhau.
  * Sử dụng CloudFormation Templates để khởi tạo VPC infrastructure.
  * Tạo và cấu hình Security Group cho phép traffic giữa 2 VPC.
  * Launch EC2 Instances trong các VPC để test connectivity.
  * Update **Network ACL (NACL)** để allow traffic giữa các subnet.
  * Cấu hình **Route Tables** trong cả 2 VPC để route traffic qua peering connection.
  * Enable **Cross-Peer DNS** để resolve DNS name giữa các VPC.
  * Test và verify connectivity giữa EC2 instances trong 2 VPC.

* **Lab20 - AWS Transit Gateway (7 bài lab)**
  * Thiết lập **AWS Transit Gateway** làm hub trung tâm để kết nối nhiều VPC.
  * Thực hiện preparation steps và planning cho Transit Gateway architecture.
  * Tạo Transit Gateway với cấu hình phù hợp cho multi-VPC environment.
  * Tạo **Transit Gateway Attachments** để gắn các VPC vào Transit Gateway.
  * Tạo và cấu hình **Transit Gateway Route Tables** để control traffic routing.
  * Update **VPC Route Tables** để route traffic qua Transit Gateway.
  * Test connectivity giữa các VPC thông qua Transit Gateway.
  * Clean up resources sau khi hoàn thành lab.

---

 Sau tuần 3, đã hoàn thành 26 bài Lab về Hybrid DNS, VPC Peering và Transit Gateway, củng cố kỹ năng networking trên AWS và hiểu rõ cách kết nối các VPC với nhau cũng như với on-premises.
