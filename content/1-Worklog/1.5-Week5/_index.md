---
title: "Week 5 Worklog"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---



### Week 5 Objectives:

* Deeply understand **Shared Responsibility Model** in AWS and differentiate security responsibilities between AWS and customers.
* Master core concepts of **AWS Identity and Access Management (IAM)**:
  * Root Account, IAM User, IAM Group, IAM Role
  * IAM Policy (Identity-based and Resource-based)
  * IAM Principal and authentication/authorization mechanisms
* Thoroughly understand **Amazon Cognito** and how to manage user authentication for web/mobile apps:
  * User Pool - Manage user registration/login
  * Identity Pool - Grant access to AWS services
* Learn **AWS Organizations** to centrally manage multiple AWS accounts:
  * Organization Unit (OU)
  * Service Control Policies (SCP)
  * Consolidated Billing
* Get familiar with **AWS Identity Center (SSO)** to centrally manage access to AWS accounts and external applications.


### Tasks to carry out this week:
| Day | Tasks                                                                                                                                                                                   | Start date | Completion date | References                            |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------- |
| 2   | - Learn **Shared Responsibility Model**: <br>&emsp; + Differentiate security responsibilities between AWS and Customer <br>&emsp; + Understand differences between Infrastructure Services, Container Services and Managed Services <br>&emsp; + Determine scope of responsibility for each AWS service type <br> - Learn **basic AWS IAM**: <br>&emsp; + Root Account and best practices for protecting Root Account <br>&emsp; + IAM User, IAM Group and credentials management <br>&emsp; + IAM Principal and authentication/authorization mechanisms | 06/10/2025   | 06/10/2025      |
| 3   | - Research **IAM Policy**: <br>&emsp; + Identity-based Policy vs Resource-based Policy <br>&emsp; + Permission evaluation mechanism: Explicit Deny > Explicit Allow <br>&emsp; + Practice writing IAM Policy for S3 bucket <br> - Learn **IAM Role**: <br>&emsp; + Difference between IAM User and IAM Role <br>&emsp; + Trust Policy and Permission Policy <br>&emsp; + Assume Role and AWS STS (Security Token Service) <br>&emsp; + Use cases: IAM Role for EC2, Lambda, Cross-account access | 07/10/2025   | 07/10/2025      | [AWS IAM Documentation](https://docs.aws.amazon.com/iam/) |
| 4   | - Learn **Amazon Cognito**: <br>&emsp; + User Pool: user registration/login, MFA, custom attributes <br>&emsp; + Identity Pool: grant access to AWS services for end users <br>&emsp; + Integrate User Pool with Identity Pool <br>&emsp; + Federated Identity with Social Login (Google, Facebook) <br> - Practice lab: <br>&emsp; + Create User Pool and test registration/login <br>&emsp; + Configure Identity Pool to access S3 | 08/10/2025   | 08/10/2025      | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/) |
| 5   | - Research **AWS Organizations**: <br>&emsp; + Organization structure: Root, OU (Organization Unit), Member Accounts <br>&emsp; + Service Control Policies (SCP): Allow-list vs Deny-list <br>&emsp; + Consolidated Billing and cost allocation <br>&emsp; + Best practices for multi-account strategy <br> - Learn **AWS Identity Center (SSO)**: <br>&emsp; + Identity Source: AWS Identity Center, Active Directory, External IdP <br>&emsp; + Permission Sets and Account assignments <br>&emsp; + Integration with AWS Managed Microsoft AD | 09/10/2025   | 09/10/2025      | [AWS Organizations](https://docs.aws.amazon.com/organizations/) <br> [AWS Identity Center](https://docs.aws.amazon.com/singlesignon/) |
| 6   | - Practice **IAM Best Practices**: <br>&emsp; + Create IAM Administrator User instead of using Root <br>&emsp; + Lock Root User credentials <br>&emsp; + Configure MFA for important accounts <br>&emsp; + Use IAM Role for applications instead of hard-coding credentials <br> - Consolidate knowledge: <br>&emsp; + Compare IAM User, IAM Group, IAM Role <br>&emsp; + Compare User Pool vs Identity Pool in Cognito <br>&emsp; + Understand relationship between Organizations, SCP and IAM Policy | 10/10/2025   | 10/10/2025      | [AWS Security Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |


### Week 5 Achievements:

* Clearly understand **Shared Responsibility Model** in AWS:
  * Differentiate security responsibilities between AWS (Security OF the Cloud) and Customer (Security IN the Cloud)
  * Understand differences in security responsibilities between Infrastructure Services, Container Services and Managed Services
  * Determine scope of responsibility for specific AWS service types

* Master **AWS IAM (Identity and Access Management)**:
  * **Root Account**: Understand importance and best practices for protecting Root Account
  * **IAM User**: Create and manage users, credentials (access key/secret key)
  * **IAM Group**: Group users for more efficient permission management
  * **IAM Policy**: Differentiate Identity-based Policy and Resource-based Policy
  * **IAM Role**: Understand difference with IAM User, how to use Trust Policy and Assume Role
  * Permission evaluation mechanism: **Explicit Deny always takes priority over Allow**

* Proficient with **IAM Role** and important use cases:
  * Grant EC2 instance access to S3 without hard-coding credentials
  * Use AWS STS (Security Token Service) to create temporary credentials
  * Cross-account access with IAM Role
  * IAM Role for AWS Services (Lambda, EC2, ECS, etc.)

* Thoroughly understand **Amazon Cognito**:
  * **User Pool**: Manage authentication (registration/login), MFA, custom attributes
  * **Identity Pool**: Grant authorization access to AWS services for end users
  * Integrate User Pool with Identity Pool for complete flow
  * Federated Identity with Social Login (Google, Facebook, SAML)
  * Practice creating User Pool and configuring Identity Pool to access S3

* Master **AWS Organizations**:
  * Organization structure: Root, Organization Unit (OU), Member Accounts
  * **Service Control Policies (SCP)**: Set maximum permission limits for accounts/OUs
  * Differentiate Allow-list and Deny-list strategies
  * **Consolidated Billing**: Centralize billing and optimize costs
  * Multi-account strategy and best practices

* Understand **AWS Identity Center (SSO)**:
  * Centrally manage access to multiple AWS accounts
  * **Identity Source**: AWS Identity Center, AWS Managed Microsoft AD, External IdP
  * **Permission Sets**: Define access permissions for users/groups
  * Integration with Active Directory (Two-way trust, AD Connector)

* Apply **IAM Best Practices**:
  * ✅ Don't use Root Account for daily work
  * ✅ Create IAM Administrator User to replace Root
  * ✅ Lock Root User access keys
  * ✅ Enable MFA (Multi-Factor Authentication) for important accounts
  * ✅ Use IAM Role for applications instead of hard-coding credentials
  * ✅ Apply Principle of Least Privilege

* Clearly understand relationships between components:
  * IAM User vs IAM Role: When to use which
  * User Pool vs Identity Pool in Cognito
  * Organizations SCP vs IAM Policy: Interaction and priority
  * Identity-based Policy vs Resource-based Policy
