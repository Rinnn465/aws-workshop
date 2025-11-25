---
title: "Week 2 Worklog"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---



### Week 2 Objectives:

* Deeply understand **Amazon VPC (Virtual Private Cloud)**: CIDR, Subnet, Route Table, ENI, Elastic IP, VPC Endpoint, Internet Gateway.
* Master knowledge of **network security on AWS**: Security Group (stateful), Network ACL (stateless), VPC Flow Logs.
* Understand and practice **VPC connection models**: VPC Peering, Transit Gateway and limitations of each method.
* Learn about **Hybrid connectivity**: VPN Site-to-Site, VPN Client-to-Site, AWS Direct Connect.
* Thoroughly understand types of **Elastic Load Balancing (ELB)**: Application Load Balancer (ALB), Network Load Balancer (NLB), Classic Load Balancer (CLB), Gateway Load Balancer (GLB) and use cases for each type.
* Practice labs on VPC and VPN Site-to-Site.

### Tasks to carry out this week:
| Day | Tasks                                                                                                                                                                                   | Start date  | Completion date | References                                |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | --------------- | ----------------------------------------- |
| 2   | - Learn theory about **Amazon VPC**: <br>&emsp; + VPC in Region, CIDR IPv4/IPv6, limit 5 VPC/Region <br>&emsp; + Subnet in Availability Zone, Route Table (Default vs Custom) <br>&emsp; + Elastic Network Interface (ENI), Elastic IP (EIP) <br>&emsp; + VPC Endpoint (Interface Endpoint vs Gateway Endpoint) <br>&emsp; + Internet Gateway (IGW) - auto scale out | 15/09/2025   | 15/09/2025      | [AWS Study Group - Module 2](https://www.youtube.com/watch?v=O9Ac_vGHquM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=25) |
| 3   | - Learn about **network security**: <br>&emsp; + Security Group (stateful, only allow rules, apply on ENI) <br>&emsp; + Network ACL (stateless, has allow/deny rules, apply on Subnet) <br>&emsp; + VPC Flow Logs (export to CloudWatch/S3) <br> - Learn about **VPC Peering**: 1:1 connection, no transitive routing, no overlapping IP <br> - Learn about **Transit Gateway**: central hub, Transit Gateway Attachment at AZ-level | 16/09/2025   | 16/09/2025      | [AWS Study Group - Module 2](https://www.youtube.com/watch?v=BPuD1l2hEQ4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=26) |
| 4   | - Learn about **VPN**: <br>&emsp; + VPN Site-to-Site (Virtual Private Gateway + Customer Gateway) <br>&emsp; + VPN Client-to-Site <br> - Learn about **AWS Direct Connect**: 20-30ms latency, Hosted Connections vs Dedicated Connections <br> - Learn details about **Elastic Load Balancing**: <br>&emsp; + Health check, Sticky session, Access logs <br>&emsp; + ALB (Layer 7, HTTP/HTTPS, path-based routing) <br>&emsp; + NLB (Layer 4, TCP/TLS, static IP, high performance) <br>&emsp; + CLB (Layer 4+7, high cost, few features) <br>&emsp; + GLB (for Security appliances) | 17/09/2025   | 17/09/2025      | [AWS Study Group - Module 2](https://www.youtube.com/watch?v=CXU8D3kyxIc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=27) |
| 5   | - Practice **Lab03** - Amazon VPC and VPN Site-to-Site (18 sub-labs): <br>&emsp; + Lab 03-1: Introduction, Subnets, Route Table, IGW, NAT Gateway <br>&emsp; + Lab 03-2: Security Group, Network ACLs, VPC Resource Map <br>&emsp; + Lab 03-3: Create VPC, Subnet, IGW, Route Table, Security Groups <br>&emsp; + Lab 03-4: Create EC2 Instances, Test connection, NAT Gateway, EC2 Instance Connect Endpoint | 18/09/2025   | 18/09/2025      | [Lab03 - VPC](https://www.youtube.com/watch?v=O5CIvG0Wt78&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=28) |


### Week 2 Achievements:

* **Knowledge about Amazon VPC**
  * Understand VPC (CIDR IPv4/IPv6, limit 5 VPC/Region), Subnet (by AZ), Route Table (Default vs Custom).
  * Understand ENI (virtual network card), EIP (static public IPv4, charged when not in use).
  * Differentiate VPC Endpoint: Interface Endpoint (ENI + Private IP) and Gateway Endpoint (Route Table, only S3/DynamoDB).
  * Understand Internet Gateway (IGW) - auto scale out.

* **Knowledge about network security**
  * Differentiate Security Group (stateful, only allow, apply on ENI) and Network ACL (stateless, allow/deny, apply on Subnet).
  * Understand VPC Flow Logs (export to CloudWatch/S3, does not capture packet content).

* **Knowledge about VPC and Hybrid connectivity**
  * VPC Peering (1:1 connection, no transitive routing, no overlapping IP).
  * Transit Gateway (central hub, Transit Gateway Attachment at AZ-level).
  * VPN Site-to-Site (Virtual Private Gateway + Customer Gateway), VPN Client-to-Site.
  * AWS Direct Connect (20-30ms latency, Hosted/Dedicated Connections).

* **Knowledge about Elastic Load Balancing**
  * Understand 4 types of ELB: ALB (Layer 7, HTTP/HTTPS, path-based routing), NLB (Layer 4, TCP/TLS, static IP, high performance), CLB (Layer 4+7, rarely used), GLB (Security appliances).
  * Understand health check, sticky session, access logs.

* **Hands-on skills**
  * Completed Lab03 (18 sub-labs): create VPC, Subnet, IGW, NAT Gateway, Security Group, NACL, EC2 Instances, Route Table, test connection.
  * Mastered the process of setting up complete VPC and configuring connections between subnets.

---

✅ After week 2, have solid foundation on Networking in AWS (VPC, Security, Routing), connection models (Peering, Transit Gateway, VPN, Direct Connect), Load Balancing (ALB, NLB, CLB, GLB) and practiced 18 labs on VPC.
