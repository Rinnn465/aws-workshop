---
title: "Blog 1"
date: "2025-11-25"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Data Protection and Security Best Practices with Veeam on AWS

Authors: Desmond Lai Xu and Vishwajeeth Venkatesh | March 11, 2025 | on [Best Practices](https://aws.amazon.com/blogs/apn/category/post-types/best-practices/), [Intermediate (200)](https://aws.amazon.com/blogs/apn/category/learning-levels/intermediate-200/), [Partner solutions](https://aws.amazon.com/blogs/apn/category/post-types/partner-solutions/), [Security & Governance](https://aws.amazon.com/blogs/apn/category/business-intelligence/security-governance/), [Security, Identity, & Compliance](https://aws.amazon.com/blogs/apn/category/security-identity-compliance/), [Storage](https://aws.amazon.com/blogs/apn/category/storage/) | [Permalink](https://aws.amazon.com/blogs/apn/data-protection-and-security-best-practices-with-veeam-on-aws/) | [Comments](https://aws.amazon.com/blogs/apn/data-protection-and-security-best-practices-with-veeam-on-aws/#Comments) | [Share](https://aws.amazon.com/blogs/apn/data-protection-and-security-best-practices-with-veeam-on-aws/#)

Safeguarding sensitive information is crucial for all organizations. With the rise in data volumes from hundreds of terabytes to petabytes, and the inclusion of sensitive Personally Identifiable Information (PII), organizations are required to meet stringent regulatory requirements with respect to data security. Organizations need to protect data and their IT landscape from misconfigurations, human errors, and evolving cyber threats such as ransomware and vulnerabilities in environments. This leaves organizations susceptible to financial, reputational, and operational damage. Common customer challenges include:

* **Insecure data backups:** Poorly configured backups leave gaps in your disaster recovery plan.
* **Data in transit vulnerabilities:** Improper encryption during transmission opens data up to interception.
* **IAM mismanagement:** Due to identity and access misconfigurations.
* **Ransomware targeting backups:** Typically in ransomware attacks, backup repositories are the first target.

These concerns highlight the critical need for robust data protection and effective cyber-resiliency strategies to mitigate risks and ensure compliance.

![][image1]

## **Data Protection Security Best Practices Overview**

When adopting AWS cloud, understanding the [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/) is crucial. This model delineates the division of security responsibilities between AWS and the customer. While AWS manages the security of the cloud infrastructure, customers are responsible for securing their data within the cloud. This includes implementing appropriate identity and access management, encryption, and network security measures. Best practices in securing your data includes:

* **Implement multi-layered and hardened backup strategies:** Ensure backups are encrypted and logically isolated from public internet avoiding exposure and risks.
* **Encrypt data in transit and at rest:** Apply standards for transit and at-rest data.
* **Strengthen IAM protocols:** Implement least privilege, multi-factor authentication (MFA), and regular audits.
* **Ransomware protection and backup isolation:** Implement immutable repositories and isolate backup data.

Veeam assists customers comply with regional, local, and industry regulations and frameworks including ([Cloud Act](https://aws.amazon.com/compliance/cloud-act/), [HIPAA](https://aws.amazon.com/compliance/hipaa-compliance/), [NIST](https://aws.amazon.com/compliance/nist/), [IRAP](https://aws.amazon.com/compliance/irap/), [MTCS Tier 3](https://aws.amazon.com/compliance/aws-multitiered-cloud-security-standard-certification), [OSPAR](https://aws.amazon.com/compliance/OSPAR/), [ISO 20000](https://aws.amazon.com/compliance/iso-20000-faqs/), and [more](https://aws.amazon.com/compliance/programs/)). Veeam implements this by seamlessly integrating with AWS-provided mechanisms and out-of-the-box solutions, enabling customers to effectively secure their AWS cloud environments.

## **Veeam Backup on AWS Implementation & Configuration**

To ensure customer data remains secure and protected against potential risks, it is crucial to align Veeam deployments on AWS with established security best practices.

In the following sections, we will explore how Veeam integrates these best practices, to mitigate security threats, and ensure compliance with industry standards and reduce customer risk profile.

### **1. Repository Immutability**

Store data in a state that cannot be modified after creation. This ensures data integrity and durability to meet audit and compliance requirements by preserving historical records and transactions ensuring data cannot be deleted or overwritten during a specific retention timeframe.

**Implementation and Integration by Veeam**

Veeam Backup for AWS allows you to protect data stored in backup repositories from deletion by making the data immutable until it reaches its desired retention period.

Veeam Backup uses [Amazon Simple Storage Service (S3) Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html) to prevent backup data deletion or modification based on retention policies. In compliance mode, data cannot be tampered or deleted by any user including the AWS account root user, protecting against ransomware and malicious actions. For configuration details, refer to [Immutability configuration guide on Veeam documentations](https://helpcenter.veeam.com/docs/vbaws/guide/immutability.html?ver=80).

![][image2]

### **2. Reducing Blast Radius / Isolation**

Physically and logically isolating data, infrastructure, and applications minimizes the impact of failures. By compartmentalizing data and workloads, organizations can better segment access permissions and reduce the attack surface, making it harder for attackers to move laterally. Isolated environments allow organizations to pinpoint the source of a problem more quickly and apply targeted solutions without affecting other parts of the system.

**Implementation and Integration by Veeam**

Veeam allows you to create a separate backup account in which all the backup infrastructure can be deployed.

This can also be deployed in a separate [AWS Region](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) for further redundancy. This ensures availability if your AWS account gets compromised and addresses any issues in geo-level availability.

![][image3]

### **3. Encryption Everywhere**

Protecting data in transit and at rest makes it unreadable to bad actors both internally and externally. Many regulatory standards and compliance frameworks require data encryption to safeguard sensitive information. By encrypting data in accordance with these requirements, organizations can ensure compliance and avoid potential penalties or legal issues.

Having encrypted backups and snapshots in a separate account and region allows customers to follow [best practices in data protection](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec-dataprot.html). Veeam automatically deploys worker instances in production or backup accounts and removes it immediately after restore and backup processes are complete. These can be deployed separately from Appliance accounts where Veeam Backup for AWS is installed and Backup Repository accounts where backup data is stored in Amazon S3.

**Implementation and Integration by Veeam**

Amazon S3 buckets are encrypted by default using Amazon S3-managed keys (SSE-S3), providing foundational data security. For additional protection, Veeam Backup for AWS allows users to encrypt backup data stored in repositories through Veeam's own encryption mechanisms.

Furthermore, Veeam extends this security by supporting native [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/) encryption for [Amazon Elastic Cloud Compute (Amazon EC2)](https://aws.amazon.com/pm/ec2/) and [Amazon Relation Database Service (Amazon RDS)](https://aws.amazon.com/rds/) instance volumes, [Amazon Elastic File System (Amazon EFS)](https://aws.amazon.com/efs/), [Amazon FSx](https://aws.amazon.com/fsx/) file systems, [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) tables, and cloud-native snapshots. Veeam uses the 256-bit Advanced Encryption Standard (AES) for its encryption process, ensuring robust protection.

Veeam Backup for AWS uses AWS KMS keys and CMKs to encrypt backup data at rest and in transit. The encryption process secures snapshots at the block level before mounting to worker instances and maintains protection throughout the S3 backup workflow, ensuring data security and compliance.

Veeam integrates seamlessly with [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) roles, ensuring that only authorized roles can access or manage encrypted backups. By enforcing encryption across all data points, Veeam simplifies managing encryption policies while bolstering the overall security of backup data.

![][image4]

### **4. Identity and Access Management**

Correct configuration of IAM ensures the right users access the right data at the right time, with [minimal levels of permission](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec_permissions_least_privileges.html) to perform a task. This provides centralized control and visibility into user access and activity across AWS services and resources, enabling organizations to monitor user behavior, detect suspicious activity, and respond to security incidents in real-time.

**Implementation and Integration by Veeam**

Veeam allows you to create granular IAM roles to perform backup and restore operations in multiple AWS accounts. Veeam enforces least privileged access, giving users and systems only the minimum level of access needed to perform only their necessary tasks, reducing the potential damage in the event of a compromise.

Veeam integrates with single sign-on providers and multi-factor authentication for enhanced security. Granular role assignments reduce compromise risks during AWS security audits. For details, refer to [Veeam Backup for AWS IAM Permissions](https://helpcenter.veeam.com/docs/vbaws/guide/system_requirements_permissions.html?ver=80) documentation for more information.

### **5. End-to-End Private Connectivity**

Private network deployment reduces security risks by preventing public internet exposure, protecting against eavesdropping and interception while improving network performance and reliability.

Dedicated connections or VPNs provide predictable bandwidth, lower latency, and higher throughput, ensuring optimal performance for mission-critical applications and workloads.

**Implementation and Integration by Veeam**

Veeam supports private deployment of backup infrastructure to ensure core backup components are secure and do not have public-facing endpoints. Veeam allows you to deploy [backup appliance in a private environment](https://helpcenter.veeam.com/docs/vbaws/guide/appliance_in_private.html?ver=80).

Additionally, Veeam can enable private network deployment functionality, allowing communication to Amazon S3 via [private Amazon S3 interface endpoints](https://docs.aws.amazon.com/AmazonS3/latest/userguide/privatelink-interface-endpoints.html). Veeam allows you to deploy [workers in private environments](https://helpcenter.veeam.com/docs/vbaws/guide/worker_instances_in_private.html?ver=80) without public IPV4 assignment which ensures backup traffic flow is secure.

If you are looking to deploy Veeam Backup for AWS in a private environment and need guidance, Veeam provides an [automation script](https://www.veeam.com/kb4552) to help you get started.

![][image5]

## **Conclusion**

Veeam®, the global market leader in data protection and ransomware recovery, is on a mission to empower organizations to not just bounce back from a data outage or loss but to bounce forward. With Veeam, organizations achieve radical resilience through data security, data recovery, and data freedom for their hybrid cloud environments. The Veeam Data Platform delivers a single solution for cloud, virtual, physical, SaaS, and Kubernetes environments, giving IT and security leaders peace of mind that their apps and data are protected and always available. Headquartered in Columbus, Ohio, with offices in more than 30 countries, Veeam protects over 450,000 customers worldwide, including 73% of the Global 2000, who trust Veeam to keep their businesses running.

Veeam on AWS provides comprehensive data protection and ransomware recovery through security best practices, enhanced by AWS's scalable infrastructure for backup and disaster recovery capabilities.

The Veeam-AWS partnership leverages S3 and Glacier Deep Archive for secure, cost-effective data protection and rapid recovery. Following AWS best practices, Veeam ensures data security, resilience, and regulatory compliance while protecting against ransomware and data loss.

[image1]: /images/3-BlogsTranslated/Blog1/image1.png

[image2]: /images/3-BlogsTranslated/Blog1/image2.png

[image3]: /images/3-BlogsTranslated/Blog1/image3.png

[image4]: /images/3-BlogsTranslated/Blog1/image4.png

[image5]: /images/3-BlogsTranslated/Blog1/image5.png
