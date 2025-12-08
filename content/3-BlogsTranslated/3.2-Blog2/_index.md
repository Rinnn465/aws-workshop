---
title: "Blog 2"
date: "2025-11-25"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---


# Effectively implementing resource control policies in a multi-account environment

Authors: Tatyana Yatskevich and Harsha Sharma | March 26, 2025 | on [Announcements](https://aws.amazon.com/blogs/security/category/post-types/announcements/), [Intermediate (200)](https://aws.amazon.com/blogs/security/category/learning-levels/intermediate-200/), [Security, Identity, & Compliance](https://aws.amazon.com/blogs/security/category/security-identity-compliance/), [Technical How-to](https://aws.amazon.com/blogs/security/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/security/effectively-implementing-resource-controls-policies-in-a-multi-account-environment/) | [Comments](https://aws.amazon.com/blogs/security/effectively-implementing-resource-controls-policies-in-a-multi-account-environment/#Comments) | [Share](https://aws.amazon.com/blogs/security/effectively-implementing-resource-controls-policies-in-a-multi-account-environment/#)

Every organization strives to empower teams to drive innovation while safeguarding their data and systems from unintended access. For organizations that have thousands of [Amazon Web Services (AWS)](https://aws.amazon.com/) resources spread across multiple accounts, organization-wide permissions guardrails can help maintain secure and compliant configurations. For example, some AWS services support [resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html) that can be used to grant identities permissions to perform actions on the resources they're attached to. With the management of resource-based policies frequently delegated to application owners, central security teams use permissions guardrails to help ensure that possible misconfigurations don't lead to unintended access to these resources.

In this post, we discuss how you can use [resource control policies (RCPs)](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps.html) to centrally restrict access to resources. We demonstrate how RCPs can help improve your security posture while allowing even more freedom to developers in managing their resources, thus reducing friction between central security and application teams. Using a sample use case, we uncover key considerations for designing and effectively implementing RCPs in your organization at scale.

If you're new to RCPs, we recommend starting with [Introducing resource control policies (RCPs), a new type of authorization policy in AWS Organizations](https://aws.amazon.com/blogs/aws/introducing-resource-control-policies-rcps-a-new-authorization-policy/), which provides an introduction to RCPs and their role in your security strategy.

## **RCP implementation journey**

RCPs are a type of authorization policy in [AWS Organizations](https://aws.amazon.com/organizations/). RCPs work alongside [service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) (SCPs) to help [establish permissions guardrails across multiple accounts](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-permissions-guardrails) in your organization. To understand their differences and use cases, see [General use cases for SCPs and RCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_authorization_policies.html#scps-rcps-general-use-cases) and [Enforcing enterprise-wide preventive controls with AWS Organizations](https://aws.amazon.com/blogs/mt/enforcing-enterprise-wide-preventive-controls-with-aws-organizations/).

We recommend implementing permissions guardrails, including RCPs, using the following iterative process, which consists of five phases (as shown in Figure 1).

1. Examine your security control objectives  
2. Design permissions guardrails  
3. Anticipate potential impacts  
4. Implement permissions guardrails  
5. Monitor permissions guardrails

![Các giai đoạn triển khai](/images/3-BlogsTranslated/Blog2/image1.png)

*Figure 1: Permissions guardrails implementation journey*

This phased approach helps ensure an effective integration of RCPs into your security strategy, improving your security posture while helping to maintain business continuity. Let's explore each phase of RCP implementation in detail and outline key considerations for an effective implementation strategy.

### **Phase 1: Examine your security control objectives**

The first step in implementing RCPs is identifying areas where RCPs can help improve your security posture or optimize the implementation of controls for your organization's specific security control objectives.

Your control objectives can be influenced by a variety of factors such as compliance and regulatory requirements, legal and contractual obligations, types of workloads, data classification, and your organization's threat model. After your control objectives are well-defined and prioritized, identify those that can be achieved using RCPs.

Like SCPs, RCPs are designed to establish coarse-grained access controls, security invariants that rarely change and serve as always-on boundaries across a wide range of AWS resources in your accounts. RCPs aren't for managing fine-grained access controls. You will keep using policies such as resource-based and identity-based policies to [apply least-privilege permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege).

More specifically, the following are key control objectives that you can achieve using RCPs:

* Establish a [data perimeter](https://aws.amazon.com/identity/data-perimeters-on-aws/) around your AWS resources. For example, you can use RCPs to help ensure that only trusted identities can access your AWS resources.  
* Mitigate the [cross-service confused deputy](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html#cross-service-confused-deputy-prevention) risk. You can use RCPs to help ensure that your AWS resources are accessed by AWS services only on behalf of your organization.  
* Apply consistent access controls to your AWS resources regardless of the identities accessing them. For example, you can use RCPs to help ensure your [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) buckets require TLS v1.2 or higher for in-transit encryption.

For additional use cases and types of controls that can be implemented using RCPs, you can explore the [resource control policy examples repository](https://github.com/aws-samples/resource-control-policy-examples). In this post, we demonstrate how to help ensure that only trusted identities can access your [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) roles.

Let's begin with the scenario illustrated in Figure 2\. Your company's central cloud team manages your corporate AWS Organizations organization, which consists of two corporate AWS accounts. An IAM principal in Account A should be able to assume an IAM role in Account B to perform day-to-day operations. To align to the broader control objective of *Only trusted identities can access my resources*, the central security team wants to make sure that the IAM role in Account B (my resource) can only be assumed by IAM principals that belong to their organization (trusted identities).

![](/images/3-BlogsTranslated/Blog2/image2.png)

*Figure 2: Simple scenario depicting a trusted identity accessing an IAM role*

One way of achieving this control objective is to follow the principle of [least-privilege](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec_permissions_least_privileges.html) and make sure that the role trust policy, the resource-based policy attached to the IAM role, only allows access to identities that require that access. The following is an example trust policy that grants permissions to Role A in Account A to assume Role B in Account B.

![](/images/3-BlogsTranslated/Blog2/image3.png)

In organizations that have only a few accounts, central teams typically manage these policies. While this centralized governance model helps ensure that trust policies applied to roles are always restricted to trusted identities, it can also impede the productivity of application teams when operating at a greater scale.

Assume that your company has started growing its cloud footprint so much that your central security team now must achieve the same control objective with hundreds of IAM roles that are spread across multiple AWS accounts, as demonstrated in Figure 3\.

![](/images/3-BlogsTranslated/Blog2/image4.png)

*Figure 3: Restricting access by managing individual IAM role trust policies*

At this scale, we see organizations delegating permissions management to application teams to better support the growth of their business and empower developers to innovate faster. While central security teams no longer have full control over the permissions granted to resources across AWS accounts, they must make sure that access is aligned with their organization's security standard. For example, they might want to make sure that the GrantCrossAccountAccess statement that is now managed by developers doesn't inadvertently grant access to an account that doesn't belong to their organization. Previously, central security teams typically achieved this by developing automated mechanisms to insert a standard statement into all trust policies. This statement helped ensure that access remained bounded to their organization, even when developers configured broad access permissions for their roles. The following is an example trust policy where a developer granted permissions to an external account through the GrantCrossAccountAccess statement. However, because of the RestrictAccessToMyOrg statement added to the policy by the central security team, the external account will be unable to use these permissions.

![](/images/3-BlogsTranslated/Blog2/image5.png)

The RestrictAccessToMyOrg statement uses the [aws:PrincipalOrgID](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-principalorgid) and [aws:PrincipalIsAWSService](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-principalisawsservice) condition keys to restrict access to principals within your organization or to [AWS service principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-services). The BoolIfExists operator with the aws:PrincipalIsAWSService condition key is required if the roles you're applying a control to are [service roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) that are used by AWS services to perform operations on your behalf. When an AWS service assumes a service role, it uses its AWS service principal, an identity that is owned by AWS and that does not belong to your organization.

The central security teams could, for example, use [AWS Config rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html) to detect misconfigurations and then use [AWS Config remediation](https://docs.aws.amazon.com/config/latest/developerguide/remediation.html) to automatically add the RestrictAccessToMyOrg statement to the IAM roles' trust policies when new IAM roles are created or their trust policies are changed. Even though the addition of the RestrictAccessToMyOrg statement to trust policies can be automated, RCPs can greatly simplify enforcement of such coarse-grained controls in a multi-account environment.

### **Phase 2: Design permissions guardrails**

After you have identified the use case you want to address and the entities or resources that you want to apply controls for, you can begin designing your RCPs. If you're new to RCPs, we strongly advise that you start your implementation journey with one use case at a time so that you can incrementally build your experience and fine-tune your controls. For the rest of this post, we will walk you through implementing an RCP that limits all of your IAM roles to being assumed by identities within your trusted perimeter. Specifically, we will examine a use case where we want to make sure that the roles in our organization can only be assumed by identities within our organization, by AWS service principals, or by a set of trusted partners who have a valid business reason to assume the roles.

**Determine an applicable attachment target**

After you have determined the control that you want to use, you need to identify the target for the control attachment to minimize the scope of impact of your RCP. RCPs currently support attachment at the root, OU, or account level. The root and OU levels provide an effective way of centralizing control management and applying controls at scale without the need to perform operations on individual accounts.

If you choose to implement the control at the OU level and you organize your accounts into OUs based on the compliance requirements applicable to them or based on a common set of controls that govern those accounts, then you can create and deploy multiple RCPs for different use cases as applicable to the sets of accounts organized within OUs. For example, as shown in Figure 2, you might have one OU for accounts that store critical data and another for the accounts that store non-critical data. You can use dedicated RCPs for these OUs to make sure that the security requirements for each specific type of data are met. Additionally, if you choose to enforce data residency using [Identity and Access Management Access Analyzer](https://aws.amazon.com/iam/access-analyzer/), you can create a dedicated OU for organizing the accounts that are subject to these requirements and apply an RCP that helps prevent creation of multi-region access points (MRAPs) for any Amazon S3 buckets in this OU, thus reducing the possibility of unintentional cross-region replication.

If you choose to implement the control at the root or OU levels, it's important to be aware that the RCP applies to all resources under the specified entity. Make sure that the control is designed correctly so that it doesn't impact resources that shouldn't be subject to the control.

Central security teams can implement permissions guardrails by creating an RCP that centrally blocks external access to IAM roles. The RCP that you will implement contains similar restrictions to the RestrictAccessToMyOrg statement that you used in the IAM trust policy.

![](/images/3-BlogsTranslated/Blog2/image6.png)

Like SCPs, you attach the RCP to an account, organizational unit (OU), or the root of your organization. After being attached, the RCP automatically applies to applicable resources—in this case, IAM roles—within the scope of that AWS Organizations entity. This centralized approach alleviates the need to modify hundreds of trust policies across multiple accounts, lowering the operational overhead for central security teams and helping ensure consistent access controls are applied at scale. RCPs also help you achieve separation of duties with developers still managing their least-privilege permissions in trust policies and administrators applying coarse-grained access controls in RCPs. If developers make configuration mistakes while managing permissions for their applications, the preventative access controls implemented using RCPs will help ensure that they stay within your organization's access control guidelines. See [How AWS enforcement code logic evaluates requests to allow or deny access](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic_policy-eval-denyallow.html) to understand how different policy types impact the authorization process.

If you're transitioning existing controls from resource-based policies to RCPs, use the opportunity to reassess the control design based on your current control objectives and the additional benefits offered by RCPs. For example, your previous controls might have been limited to specific resource types, such as IAM roles in this use case, or to particular accounts, such as those storing the most sensitive data. RCPs enable you to extend controls to additional resources across your entire organization, reducing operational overhead through centralized management of permissions guardrails.

If you need to apply a control on resources not yet covered by RCPs, you can implement or retain your custom automation for enforcing controls with resource-based policies. See the [List of AWS services that support RCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps.html#rcp-supported-services) and [Resources and entities not restricted by RCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps.html#actions-not-restricted-by-rcps) and plan for additional controls if applicable.

While designing your RCPs, consider the following guidelines.

**Design for operational excellence**

A key foundation for effectively implementing and operating permissions guardrails like RCPs is [organizing your AWS environment using multiple accounts](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/organizing-your-aws-environment.html). Account boundaries and strategic placement of workloads across them allow you to apply tailored access controls that align with data sensitivity and specific access requirements. Grouping accounts into OUs within AWS Organizations enables more effective access control, even in scenarios where cross-account access is required. Figure 4 illustrates an example organization structure, demonstrating how RCPs can be applied at various levels of the organizational hierarchy to adhere to the security requirements of different workloads.

![](/images/3-BlogsTranslated/Blog2/image7.png)
*Figure 4: A sample organization with RCPs applied at various levels*

When operating at scale, consider delegating policy management to a central security account in your organization. With [AWS Organizations resource-based delegation](https://docs.aws.amazon.com/organizations/latest/userguide/orgs-policy-delegate.html), central teams don't need access to the management account for any SCP or RCP related changes or troubleshooting.

Review [Achieving operational excellence with design considerations for AWS Organizations SCPs](https://aws.amazon.com/blogs/mt/achieving-operational-excellence-with-design-considerations-for-aws-organizations-scps/), which focuses on SCPs but also covers foundational principles for designing and implementing permissions guardrails at scale. These considerations also apply to RCPs for enabling operational excellence. Additionally, see [AWS Organizations quotas](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_reference_limits.html) and [RCP evaluation](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps_evaluation.html) for the RCP-related quotas and unique implementation details.

**Define your governance**

Establishing clear governance helps you define how to implement and continuously manage RCPs within your organization. This includes the operating model, change management processes, and exceptions handling procedures. RCPs provide authorization controls similar to SCPs and therefore should integrate with your existing governance framework rather than requiring separate oversight. For example, if your change management process requires two-person approval for SCP changes, you should consider applying the same approval process for RCP implementation. You should also adopt the same mechanisms you currently use to prevent unauthorized changes or detect drifts in your policies.

**Plan for exceptions**

There might be scenarios where you have a few resources that should be accessible publicly or by identities that don't belong to your organization. If you're organizing your resources across multiple accounts and OUs based on their compliance requirements or a common set of controls, then you most likely have such resources in a dedicated set of accounts or OUs, such as the *Public Data* OU in Figure 4\. These accounts or OUs can have applicable policies that account for their unique access requirements.

Another option to accommodate these scenarios is to use the [aws:ResourceAccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-resourceaccount) or [aws:ResourceOrgPaths](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-resourceorgpaths) condition key to exclude certain accounts from the control. For example, the following policy will deny access to identities outside your organization from assuming IAM roles unless the identity is an AWS service principal or the role that is being accessed belongs to Account A.

![](/images/3-BlogsTranslated/Blog2/image8.png)  
There also might be situations where your company's trusted partners or acquisitions need to be granted an exception for access to a subset of your company's resources distributed across multiple accounts. For example, your company might integrate with Cloud Security Posture Management (CSPM) tools that assume roles in your accounts to assess your accounts' security posture, as shown in Figure 5\.  
![](/images/3-BlogsTranslated/Blog2/image9.png)  
*Figure 5: Representative view of granting exceptions to trusted partners*

When implementing a control with an RCP that by default will apply to all resources of the entity it's attached to, you can manage resource specific exceptions using the aws:ResourceTag condition key. In addition, use the aws:PrincipalAccount context key to conditionally grant exceptions based on the AWS account ID of the trusted partner.

![](/images/3-BlogsTranslated/Blog2/image10.png)

Let's examine the two statements in the preceding RCP:

* RestrictAccessToMyOrgExceptTaggedRoles  
  This statement helps ensure that your roles can only be assumed by identities that belong to your organization or by AWS service principals, unless a role is tagged with partner-access-exception set to trusted-partner.  
* RestrictAccessForTaggedRoles  
  This statement further restricts access by helping ensure that the roles that have the partner-access-exception tag can only be assumed by identities that belong to your trusted partner account.

If you have a well-known, tightly scoped set of resources that need to be excluded, you can also use the IAM policy element, [NotResource](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_notresource.html), to list the Amazon Resource Names (ARNs) of resources to exclude from the control.

When implementing tag-based exception processes, establishing strict controls over tag management is key. Unauthorized modifications of tags on resources, principals, or sessions could impact your security posture by enabling unintended access. You should implement controls to help prevent unauthorized tag manipulation. For example, the following SCP restricts the use of the partner-access-exception tag to the admin role so that unauthorized users cannot alter the control by attaching, detaching, or modifying the tag.

![](/images/3-BlogsTranslated/Blog2/image11.png)

You should also make sure that the partner-access-exception tag cannot be passed as a [session tag](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_session-tags.html) when identities assume roles. See the sample [RCP](https://github.com/aws-samples/data-perimeter-policy-examples/blob/main/resource_control_policies/data_perimeter_governance_rcp.json) in the data perimeter policy examples repository.

### **Phase 3: Anticipate potential impacts**

Before rolling out RCPs, you need to understand their potential impact on your organization. Introducing new policies or modifying existing ones without proper validation can disrupt your security-productivity balance. Be aware that overly restrictive policies might inadvertently impede legitimate data flows that are essential for achieving your business objectives.

Consider using [AWS Identity and Access Management Access Analyzer](https://aws.amazon.com/iam/access-analyzer/) to monitor effective permissions across resources in your organization. For our IAM role example, use an organization external access analyzer to [identify IAM roles in your organization that are shared with external entities](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html#what-is-access-analyzer-resource-identification). This analysis will help you to create appropriate exceptions or lock down any overly permissive access.

Another effective method to assess impact is to review and analyze your account activity using [AWS CloudTrail](https://aws.amazon.com/cloudtrail/). For example, if you centralize all your CloudTrail logs in an S3 bucket, you can use [Amazon Athena](https://aws.amazon.com/athena/) to query these logs. Specifically, look for STS API calls made against your IAM roles by identities outside your organization. Then, compare the results with your list of known trusted partners and those you have already accounted for in your RCPs. Based on this analysis, determine if you need to add the partner-access-exception tag to additional IAM roles and further refine the policy before enforcement. This is essential to ensure trusted partner integrations continue to function as expected when you enforce your RCPs. Furthermore, use this analysis to identify any illegitimate access patterns in your environment and plan for necessary remediations, further enhancing your security posture as part of RCP implementation.

For detailed guidance on how to perform an impact analysis in your environment, see [Analyze your account activity to evaluate impact and refine controls](https://aws.amazon.com/blogs/security/establishing-a-data-perimeter-on-aws-analyze-your-account-activity-to-evaluate-impact-and-refine-controls/), which describes the tools and options you need to be able to conduct the analysis.

### **Phase 4: Implement permissions guardrails**

As you transition into the implementation phase, consider the following key factors to promote a smooth rollout while enhancing your security posture.

Deployment automation and integration

Use your existing deployment pipelines to implement RCPs, the same as you do for SCPs. This approach will minimize operational overhead while maintaining consistency in the deployment of your controls.

You can use the [AWS CloudFormation](https://aws.amazon.com/cloudformation/) [AWS::Organizations::Policy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-organizations-policy.html) resource type to deploy RCPs as infrastructure as code (IaC) using your continuous integration and continuous delivery (CI/CD) pipeline. If you're using [AWS Control Tower](https://aws.amazon.com/controltower/) and the [Customizations for AWS Control Tower solution (CfCT)](https://docs.aws.amazon.com/controltower/latest/userguide/customize-landing-zone.html) for account management and want to deploy your custom RCPs, use rcp as the deploy\_method in the [CfCT manifest file](https://docs.aws.amazon.com/controltower/latest/userguide/cfct-manifest-file-resources-section.html). You can also take advantage of the AWS Control Tower provided [RCP-based controls](https://docs.aws.amazon.com/controltower/latest/controlreference/list-of-rcp-controls.html) to streamline the implementation.

Progressive deployment in stages

As with SCPs, AWS strongly advises against attaching RCPs in production environments without thoroughly testing the impact that the policies have on resources in your accounts. Follow [standard CI/CD processes](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-cicd-litmus/introduction.html) and begin your RCP rollout in [lower environments](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-cicd-litmus/apg-gloss.html#glossary-environment) by attaching them to individual test accounts or OUs first. After you validate that the controls behave as excepted, gradually promote the RCPs to upper environments.

If your goal is to transition an existing control from resource-based policies to RCPs, keep your resource-based policies in place while conducting the progressive rollout. After you have completed rolling out your RCPs and confirmed that they operate as expected, you can consider deactivating the automation you used to apply the control using resource-based policies. This approach lets you deploy RCPs without impacting your existing security posture or disrupting business workflows.

Additionally, consider deploying RCPs to a subset of resources or accounts first to limit the scope of impact and provide an opportunity to test and refine your deployment and operational processes. You can follow your standard prioritization approach to define deployment waves, for example, start with resources or accounts that store sensitive data or pose the highest risk, based on your current operational practices and other controls that might be in place. For additional best practices, see [OPS06-BP03 Employ safe deployment strategies](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/ops_mit_deploy_risks_deploy_mgmt_sys.html) in the [AWS Well-Architected Framework: Operation Excellence Pillar](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/welcome.html) whitepaper.

### **Phase 5: Monitor permissions guardrails**

Finally, establish monitoring processes to help ensure that controls for preventing external access to your resources operate as expected. You can use the same tools you used for impact analysis. For example, you can use [IAM Access Analyzer external access findings](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-findings-view.html#access-analyzer-findings-view-external) to understand the impact of your RCPs on resource permissions. This information will help you verify that your RCPs are crafted in accordance with your intent and plan remediation actions, if required. You can also set alerts for occurrences of unintended access patterns observed in your CloudTrail logs.

Furthermore, follow the phased approach outlined in this post to regularly review and update your controls to help ensure that they align with evolving business and security objectives. Consider factors such as organizational changes, changes in partner relationships, data criticality shifts, and opportunities for expanding your RCP coverage. This continuous improvement process helps maintain the effectiveness of your security controls while supporting business growth and transformation.

## **Conclusion**

In this post, we discussed how to effectively implement coarse-grained access controls on AWS resources at scale using RCPs. You can use the phased implementation approach described here to achieve your security control objectives while minimizing the risk of disrupting your business workflows. You can apply the same approach to implement other preventative controls, such as SCPs, across your multi-account environment.

Remember that RCPs, like SCPs, provide a powerful mechanism for enforcing coarse-grained controls across multiple accounts in your organization. They don't replace your least-privilege controls and should be part of a broader, multi-layered approach to data security that includes other [well-architected security design principles](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html).

   
If you have feedback about this post, submit comments in the Comments section below. If you have questions about this post, [contact AWS Support](https://console.aws.amazon.com/support/home).

