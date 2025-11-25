---
title: "Worklog Tuần 5"
date: "2025-09-09"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---



### Mục tiêu tuần 5:

* Hiểu sâu về **Shared Responsibility Model** trong AWS và phân biệt trách nhiệm bảo mật giữa AWS và khách hàng.
* Nắm vững các khái niệm cốt lõi của **AWS Identity and Access Management (IAM)**:
  * Root Account, IAM User, IAM Group, IAM Role
  * IAM Policy (Identity-based và Resource-based)
  * IAM Principal và cơ chế xác thực/phân quyền
* Hiểu rõ về **Amazon Cognito** và cách quản lý xác thực người dùng cho ứng dụng web/mobile:
  * User Pool - Quản lý đăng ký/đăng nhập người dùng
  * Identity Pool - Cấp quyền truy cập vào các dịch vụ AWS
* Tìm hiểu **AWS Organizations** để quản lý tập trung nhiều AWS accounts:
  * Organization Unit (OU)
  * Service Control Policies (SCP)
  * Consolidated Billing
* Làm quen với **AWS Identity Center (SSO)** để quản lý quyền truy cập tập trung vào AWS accounts và ứng dụng bên ngoài.


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu **Shared Responsibility Model**: <br>&emsp; + Phân biệt trách nhiệm bảo mật giữa AWS và Customer <br>&emsp; + Hiểu sự khác biệt giữa Infrastructure Services, Container Services và Managed Services <br>&emsp; + Xác định phạm vi trách nhiệm cho từng loại dịch vụ AWS <br> - Tìm hiểu **AWS IAM cơ bản**: <br>&emsp; + Root Account và best practices bảo vệ Root Account <br>&emsp; + IAM User, IAM Group và cách quản lý credentials <br>&emsp; + IAM Principal và cơ chế authentication/authorization | 06/10/2025   | 06/10/2025      |
| 3   | - Nghiên cứu **IAM Policy**: <br>&emsp; + Identity-based Policy vs Resource-based Policy <br>&emsp; + Cơ chế đánh giá quyền: Explicit Deny > Explicit Allow <br>&emsp; + Thực hành viết IAM Policy cho S3 bucket <br> - Tìm hiểu **IAM Role**: <br>&emsp; + Sự khác biệt giữa IAM User và IAM Role <br>&emsp; + Trust Policy và Permission Policy <br>&emsp; + Assume Role và AWS STS (Security Token Service) <br>&emsp; + Use case: IAM Role cho EC2, Lambda, Cross-account access | 07/10/2025   | 07/10/2025      | [AWS IAM Documentation](https://docs.aws.amazon.com/iam/) |
| 4   | - Tìm hiểu **Amazon Cognito**: <br>&emsp; + User Pool: đăng ký/đăng nhập người dùng, MFA, custom attributes <br>&emsp; + Identity Pool: cấp quyền truy cập AWS services cho end users <br>&emsp; + Tích hợp User Pool với Identity Pool <br>&emsp; + Federated Identity với Social Login (Google, Facebook) <br> - Thực hành lab: <br>&emsp; + Tạo User Pool và test đăng ký/đăng nhập <br>&emsp; + Cấu hình Identity Pool để truy cập S3 | 08/10/2025   | 08/10/2025      | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/) |
| 5   | - Nghiên cứu **AWS Organizations**: <br>&emsp; + Organization structure: Root, OU (Organization Unit), Member Accounts <br>&emsp; + Service Control Policies (SCP): Allow-list vs Deny-list <br>&emsp; + Consolidated Billing và cost allocation <br>&emsp; + Best practices cho multi-account strategy <br> - Tìm hiểu **AWS Identity Center (SSO)**: <br>&emsp; + Identity Source: AWS Identity Center, Active Directory, External IdP <br>&emsp; + Permission Sets và Account assignments <br>&emsp; + Tích hợp với AWS Managed Microsoft AD | 09/10/2025   | 09/10/2025      | [AWS Organizations](https://docs.aws.amazon.com/organizations/) <br> [AWS Identity Center](https://docs.aws.amazon.com/singlesignon/) |
| 6   | - Thực hành **IAM Best Practices**: <br>&emsp; + Tạo IAM Administrator User thay vì dùng Root <br>&emsp; + Khóa credentials của Root User <br>&emsp; + Cấu hình MFA cho tài khoản quan trọng <br>&emsp; + Sử dụng IAM Role cho applications thay vì hard-code credentials <br> - Tổng hợp kiến thức: <br>&emsp; + So sánh IAM User, IAM Group, IAM Role <br>&emsp; + So sánh User Pool vs Identity Pool trong Cognito <br>&emsp; + Hiểu mối quan hệ giữa Organizations, SCP và IAM Policy | 10/10/2025   | 10/10/2025      | [AWS Security Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |


### Kết quả đạt được tuần 5:

* Hiểu rõ **Shared Responsibility Model** trong AWS:
  * Phân biệt trách nhiệm bảo mật giữa AWS (Security OF the Cloud) và Customer (Security IN the Cloud)
  * Nắm được sự khác biệt về trách nhiệm bảo mật giữa Infrastructure Services, Container Services và Managed Services
  * Xác định được phạm vi trách nhiệm cho từng loại dịch vụ AWS cụ thể

* Nắm vững **AWS IAM (Identity and Access Management)**:
  * **Root Account**: Hiểu tầm quan trọng và best practices bảo vệ Root Account
  * **IAM User**: Tạo và quản lý user, credentials (access key/secret key)
  * **IAM Group**: Nhóm user để quản lý quyền hiệu quả hơn
  * **IAM Policy**: Phân biệt Identity-based Policy và Resource-based Policy
  * **IAM Role**: Hiểu sự khác biệt với IAM User, cách sử dụng Trust Policy và Assume Role
  * Cơ chế đánh giá quyền: **Explicit Deny luôn ưu tiên hơn Allow**

* Thành thạo **IAM Role** và các use case quan trọng:
  * Cấp quyền cho EC2 instance truy cập S3 mà không cần hard-code credentials
  * Sử dụng AWS STS (Security Token Service) để tạo temporary credentials
  * Cross-account access với IAM Role
  * IAM Role for AWS Services (Lambda, EC2, ECS, etc.)

* Hiểu rõ **Amazon Cognito**:
  * **User Pool**: Quản lý authentication (đăng ký/đăng nhập), MFA, custom attributes
  * **Identity Pool**: Cấp quyền authorization vào AWS services cho end users
  * Tích hợp User Pool với Identity Pool để có luồng hoàn chỉnh
  * Federated Identity với Social Login (Google, Facebook, SAML)
  * Thực hành tạo User Pool và cấu hình Identity Pool để truy cập S3

* Nắm vững **AWS Organizations**:
  * Cấu trúc tổ chức: Root, Organization Unit (OU), Member Accounts
  * **Service Control Policies (SCP)**: Thiết lập giới hạn quyền tối đa cho accounts/OUs
  * Phân biệt Allow-list và Deny-list strategies
  * **Consolidated Billing**: Tập trung thanh toán và tối ưu chi phí
  * Multi-account strategy và best practices

* Hiểu về **AWS Identity Center (SSO)**:
  * Quản lý truy cập tập trung vào nhiều AWS accounts
  * **Identity Source**: AWS Identity Center, AWS Managed Microsoft AD, External IdP
  * **Permission Sets**: Định nghĩa quyền truy cập cho users/groups
  * Tích hợp với Active Directory (Two-way trust, AD Connector)

* Áp dụng **IAM Best Practices**:
  * ✅ Không sử dụng Root Account cho công việc hàng ngày
  * ✅ Tạo IAM Administrator User để thay thế Root
  * ✅ Khóa access keys của Root User
  * ✅ Bật MFA (Multi-Factor Authentication) cho accounts quan trọng
  * ✅ Sử dụng IAM Role cho applications thay vì hard-code credentials
  * ✅ Áp dụng Principle of Least Privilege

* Hiểu rõ mối quan hệ giữa các thành phần:
  * IAM User vs IAM Role: Khi nào dùng cái nào
  * User Pool vs Identity Pool trong Cognito
  * Organizations SCP vs IAM Policy: Sự tương tác và ưu tiên
  * Identity-based Policy vs Resource-based Policy  


