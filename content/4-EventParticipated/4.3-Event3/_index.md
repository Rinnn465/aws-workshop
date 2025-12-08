---
title: "Event 3"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---


# Event Takeaways: "AWS Cloud Mastery Series #3: AWS Well-Architected – Security Pillar Workshop"

### Program Focus
This workshop revolved around the security pillar within the AWS Well-Architected Framework, delivering an in-depth exploration of five critical security areas:

- Area 1: Identity & Access Management (IAM)
- Area 2: Continuous Monitoring & Detection
- Area 3: Infrastructure Protection
- Area 4: Data Security
- Area 5: Incident Response
  
Additionally, the session featured an overview of the AWS Cloud Clubs initiative and community-driven programs that foster cloud learning in academic settings.

### Speakers

- **Le Vu Xuan An** - AWS Cloud Club Captain HCMUTE
- **Tran Duc Anh** - AWS Cloud Club Captain SGU
- **Tran Doan Cong Ly** - AWS Cloud Club Captain PTIT
- **Danh Hoang Hieu Nghi** - AWS Cloud Club Captain HUFLIT

- **Huynh Hoang Long** - AWS Community Builders
- **Dinh Le Hoang Anh** - AWS Community Builders

- **Nguyen Tuan Thinh** - Cloud Engineer Trainee
- **Nguyen Do Thanh Dat** - Cloud Engineer Trainee

- **Van Hoang Kha** - Cloud Security Engineer, AWS Community Builder

- **Thinh Lam** - FCJ Member
- **Viet Nguyen** - FCJ Member

- **Mendel Grabski (Long)** - Ex-Head of Security & DevOps, Cloud Security Solution Architect
- **Tinh Truong** - Platform Engineer at TymeX, AWS Community Builder 

### Key Highlights

#### Launching with AWS Cloud Club
The program kicked off with an introduction to the AWS Cloud Club program:
- An environment for cultivating cloud computing capabilities through hands-on projects

- Direct access to mentorship from AWS industry experts

- Building networks and fostering collaboration among student communities

- Operated by clubs at HCMUTE, SGU, PTIT, and HUFLIT

Core message: Cloud Clubs serve as a bridge for students to mature professionally, technically, and in their career relationships.


#### Identity & Access Management (IAM)
IAM emerged as one of the workshop's most critical topics. Primary insights included:
- Implement the principle of Least Privilege

- Delete root access keys immediately following initial configuration

- Minimize wildcard permission usage (*)

- Deploy AWS SSO for unified permission control across multiple accounts

- Master SCPs as organizational-level permission constraints

- Utilize Permission Boundaries to restrict user and role capabilities

The session provided detailed analysis of two MFA approaches—TOTP and FIDO2—examining their respective security strengths and recovery mechanisms.

The Secrets Manager credential rotation workflow (create → set → test → finalize) was highlighted as an essential practice for secure credential management.


#### Continuous Monitoring & Detection
This module explained AWS's approach to establishing multi-tiered observability:
- Management Events (API invocations, configuration modifications)

- Data Events (object-level operations on S3, Lambda execution records)

- Network Events (VPC Flow Logs)

- Unified visibility spanning all organizational accounts

EventBridge received significant attention regarding alerting and automation—particularly its cross-account event routing capability for building centralized security workflows.

The "Detection-as-Code" methodology was illustrated through CloudTrail Lake and IaC-based deployment of detection logic.


#### Amazon GuardDuty
GuardDuty was presented as a fully managed threat intelligence service that examines CloudTrail events, VPC Flow Logs, and DNS queries to identify risks including logging deactivation, abnormal network patterns, or suspicious domain requests.

The workshop also explored enhanced capabilities such as malware detection for S3, EKS audit log analysis, RDS anomaly identification, Lambda network inspection, and runtime safeguards through the GuardDuty Agent.

Speakers demonstrated how GuardDuty aligns with established frameworks including AWS Foundational Security Best Practices and CIS Benchmarks.


#### Network Security Management
Infrastructure protection content encompassed:

- Attack classifications: Ingress, Egress, and Insider threats

- Contrasting Security Groups (stateful) with NACLs (stateless)

- Implementing Route 53 Resolver for hybrid environment DNS

- AWS Network Firewall applications: egress control, network segmentation, IDS/IPS

- Combining GuardDuty threat intelligence for automatic threat blocking


#### Data Security & Governance
The module emphasized the importance of encryption and credential management in AWS:
- KMS architecture (CMK → Data Key)

- Leveraging IAM conditions to restrict encryption operations

- ACM for automated certificate provisioning and renewal

- Credential rotation workflows via Secrets Manager

- Mandating TLS for S3 and DynamoDB access

- Configuring SSL/TLS on RDS with server verification

#### Incident Response & Prevention
Prevention Guidelines: The session stressed prioritizing temporary credentials, preventing public S3 bucket exposure, placing sensitive services within private subnets, applying IaC to maintain consistency, and implementing dual-layer approval for high-risk modifications (code review combined with deployment pipeline).

Response Workflow: The workshop presented a five-phase approach: advance preparation, detection and analysis, threat containment through resource isolation or access revocation, system restoration during eradication and recovery, and post-incident knowledge documentation.


### Practical Application
Security principles learned from this workshop can be directly integrated into our AI Chatbot development. Enhanced IAM practices enable tighter access management for backend systems and administrative interfaces. The emphasis on logging, monitoring, and infrastructure safeguards provides our team with a concrete framework for tracking system behavior and minimizing configuration errors. The incident response structure allows our team to address issues more promptly and methodically. Collectively, these insights contribute to building a more robust and trustworthy chatbot platform.

### Event Impressions
- The program was professionally organized with expert speakers who made complex security concepts accessible.
- Interactive discussion segments enabled participants to resolve questions and strengthen comprehension.

#### Some event photos
![Event 3-1](/images/4-EventParticipated/event3-1.jpg)
![Event 3-2](/images/4-EventParticipated/event3-2.jpg)
