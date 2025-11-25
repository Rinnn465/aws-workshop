---
title: "Week 3 Worklog"
date: "2025-09-09"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---



### Week 3 Objectives:

* Practice labs on **Route 53 Resolver** to set up Hybrid DNS between AWS and on-premises.
* Practice **VPC Peering** to connect 2 VPCs, configure Security Groups, NACLs, Route Tables and Cross-Peer DNS.
* Practice **AWS Transit Gateway** to connect multiple VPCs through a central hub, configure Transit Gateway Attachments and Route Tables.
* Strengthen Networking knowledge on AWS through hands-on labs.

### Tasks to carry out this week:
| Day | Tasks                                                                                                                                                                                   | Start date  | Completion date | References                                |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | --------------- | ----------------------------------------- |
| 2   | - Practice **Lab10** - Hybrid DNS with Route 53 Resolver (11 sub-labs): <br>&emsp; + Lab10-01: Introduction - Learn about Hybrid DNS <br>&emsp; + Lab10-02.1: Generate Key Pair <br>&emsp; + Lab10-02.2: Initialize CloudFormation Template <br>&emsp; + Lab10-02.3: Configure Security Group <br>&emsp; + Lab10-03: Connect to RDGW (Remote Desktop Gateway) <br>&emsp; + Lab10-05: Set up DNS <br>&emsp; + Lab10-05.1: Create Route 53 Outbound Endpoint <br>&emsp; + Lab10-05.2: Create Route 53 Resolver Rules <br>&emsp; + Lab10-05.3: Create Route 53 Inbound Endpoints <br>&emsp; + Lab10-05.4: Test results <br>&emsp; + Lab10-06: Clean up resources | 22/09/2025   | 22/09/2025      | [Lab10 - Route 53 Resolver](https://www.youtube.com/watch?v=FGicpWOmMDI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=45) <br> (https://000010.awsstudygroup.com/) | 
| 3   | - Practice **Lab19** - VPC Peering (8 sub-labs): <br>&emsp; + Lab19-1: Introduction - Set up VPC Peering <br>&emsp; + Lab19-2.1: Initialize CloudFormation Templates <br>&emsp; + Lab19-2.2: Create Security Group <br>&emsp; + Lab19-2.3: Create EC2 Instance <br>&emsp; + Lab19-3: Update Network ACL (NACLs) <br>&emsp; + Lab19-4: Create a Peering Connection <br>&emsp; + Lab19-5: Configure Route Tables <br>&emsp; + Lab19-6: Enable Cross-Peer DNS | 23/09/2025   | 23/09/2025     | [Lab19 - VPC Peering](https://www.youtube.com/watch?v=sllYqAECBoM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=56) <br> (https://000019.awsstudygroup.com/) |
| 4   | - Practice **Lab20** - AWS Transit Gateway (7 sub-labs): <br>&emsp; + Lab20-1: Introduction - Set up AWS Transit Gateway <br>&emsp; + Lab20-2: Preparation steps <br>&emsp; + Lab20-3: Create Transit Gateway <br>&emsp; + Lab20-4: Create Transit Gateway Attachments <br>&emsp; + Lab20-5: Create Transit Gateway Route Tables <br>&emsp; + Lab20-6: Add Transit Gateway Routes to VPC Route Tables <br>&emsp; + Lab20-7: Clean up resources | 25/09/2025  | 25/09/2025     | [Lab20 - Transit Gateway](https://www.youtube.com/watch?v=ybLa49z7FFg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=65) <br> (https://000020.awsstudygroup.com/) |


### Week 3 Achievements:

* **Lab10 - Hybrid DNS with Route 53 Resolver (11 sub-labs)**
  * Set up Hybrid DNS to connect DNS between AWS VPC and on-premises data center.
  * Create and configure **Route 53 Outbound Endpoint** to resolve domain names from VPC to on-premises.
  * Create and configure **Route 53 Inbound Endpoint** to resolve domain names from on-premises to VPC.
  * Create **Route 53 Resolver Rules** to route DNS queries.
  * Use CloudFormation to initialize infrastructure, configure Security Groups for DNS traffic.
  * Connect to Remote Desktop Gateway (RDGW) to manage Windows environment.
  * Test results and verify DNS resolution works correctly between the 2 environments.

* **Lab19 - VPC Peering (8 sub-labs)**
  * Set up **VPC Peering Connection** to connect 2 VPCs together.
  * Use CloudFormation Templates to initialize VPC infrastructure.
  * Create and configure Security Groups to allow traffic between 2 VPCs.
  * Launch EC2 Instances in VPCs to test connectivity.
  * Update **Network ACL (NACL)** to allow traffic between subnets.
  * Configure **Route Tables** in both VPCs to route traffic through peering connection.
  * Enable **Cross-Peer DNS** to resolve DNS names between VPCs.
  * Test and verify connectivity between EC2 instances in 2 VPCs.

* **Lab20 - AWS Transit Gateway (7 sub-labs)**
  * Set up **AWS Transit Gateway** as central hub to connect multiple VPCs.
  * Perform preparation steps and planning for Transit Gateway architecture.
  * Create Transit Gateway with appropriate configuration for multi-VPC environment.
  * Create **Transit Gateway Attachments** to attach VPCs to Transit Gateway.
  * Create and configure **Transit Gateway Route Tables** to control traffic routing.
  * Update **VPC Route Tables** to route traffic through Transit Gateway.
  * Test connectivity between VPCs through Transit Gateway.
  * Clean up resources after completing lab.

---

✅ After week 3, completed 26 labs on Hybrid DNS, VPC Peering and Transit Gateway, strengthened networking skills on AWS and understand how to connect VPCs together and with on-premises.