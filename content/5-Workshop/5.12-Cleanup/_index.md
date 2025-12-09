---
title : "Clean Up Resources"
date :  "2025-09-09" 
weight : 12
chapter : false
pre : " <b> 5.12. </b> "
---

## Clean Up Resources

To avoid incurring unnecessary AWS charges, follow these steps to completely remove all resources created during this workshop.

{{% notice warning %}}
This cleanup process is **irreversible**. All data, including customer information, appointments, and consultant records will be permanently deleted. Make sure to export any data you need before proceeding.
{{% /notice %}}

### Step 1: Destroy CDK Stack

Navigate to your project directory and destroy the CDK stack:

```bash
cd MeetAssist
cdk destroy --all
```

When prompted, confirm the deletion by typing `y`.

This will remove:
- Lambda functions
- API Gateway
- RDS PostgreSQL database
- DynamoDB tables
- Cognito User Pools
- S3 buckets (except those with versioning/retention)
- CloudFront distributions
- SQS queues
- EventBridge rules
- IAM roles and policies

{{% notice info %}}
The CDK destroy process may take 30-40 minutes to complete. Wait for confirmation before proceeding to the next step.
{{% /notice %}}

### Step 2: Delete S3 Buckets

Some S3 buckets may not be automatically deleted if they contain objects. Manually delete them:

**List your buckets:**
```bash
aws s3 ls | grep meetassist
```

**Empty and delete each bucket:**
```bash
aws s3 rm s3://meetassist-data-<account-id>-ap-northeast-1 --recursive
aws s3 rb s3://meetassist-data-<account-id>-ap-northeast-1

aws s3 rm s3://meetassist-dashboard-<account-id>-ap-northeast-1 --recursive
aws s3 rb s3://meetassist-dashboard-<account-id>-ap-northeast-1
```

Replace `<account-id>` with your actual AWS account ID.

### Step 3: Remove Cognito Users

If you manually created any Cognito users that weren't deleted:

```bash
aws cognito-idp list-users --user-pool-id <your-user-pool-id> --region ap-northeast-1
```

The CDK destroy should have removed the User Pool, but verify in the console that no orphaned resources remain.

### Step 4: Delete Secrets Manager Secrets

Check for any remaining secrets:

```bash
aws secretsmanager list-secrets --region ap-northeast-1 | grep meetassist
```

Delete any found secrets:

```bash
aws secretsmanager delete-secret --secret-id MeetAssist/Facebook/PageAccessToken --region ap-northeast-1 --force-delete-without-recovery
aws secretsmanager delete-secret --secret-id MeetAssist/Facebook/VerifyToken --region ap-northeast-1 --force-delete-without-recovery
```

### Step 5: Delete SSM Parameters

Remove the Facebook App ID and App Secret:

```bash
aws ssm delete-parameter --name /MeetAssist/Facebook/AppId --region ap-northeast-1
aws ssm delete-parameter --name /MeetAssist/Facebook/AppSecret --region ap-northeast-1
```

### Step 6: Remove Facebook App Configuration

1. Go to [Facebook Developers](https://developers.facebook.com/)
2. Navigate to your MeetAssist app
3. Go to **Settings** → **Basic**
4. Scroll down and click **Delete App**
5. Confirm the deletion

{{% notice tip %}}
Alternatively, you can keep the Facebook App but remove the webhook subscription and page connection if you plan to rebuild the project later.
{{% /notice %}}

### Step 7: Disable Bedrock Models (Optional)

If you no longer need access to the Bedrock models:

1. Go to AWS Console → **Amazon Bedrock**
2. Navigate to **Model access** in the left sidebar
3. For each enabled model:
   - Claude 3.5 Sonnet
   - Claude 3 Sonnet
   - Claude 3 Haiku
   - Titan Embeddings G1 - Text
4. Click **Manage** → **Disable access**

{{% notice info %}}
Bedrock model access itself doesn't incur charges. You're only billed for API calls. You can leave the models enabled if you plan to use them in other projects.
{{% /notice %}}

### Step 8: Verify Cleanup

Double-check that all resources are removed:

**Check CloudFormation Stacks:**
```bash
aws cloudformation list-stacks --region ap-northeast-1 | grep MeetAssist
```

**Check Lambda Functions:**
```bash
aws lambda list-functions --region ap-northeast-1 | grep MeetAssist
```

**Check RDS Instances:**
```bash
aws rds describe-db-instances --region ap-northeast-1 | grep meetassist
```

**Check DynamoDB Tables:**
```bash
aws dynamodb list-tables --region ap-northeast-1 | grep MeetAssist
```

All commands should return empty results.

### Cost Considerations

After cleanup, you should see the following in your AWS billing:

**Ongoing Charges (None):**
- Lambda, API Gateway, RDS, DynamoDB - **$0** (resources deleted)
- CloudFront - **$0** (distribution deleted)
- S3 storage - **$0** (buckets emptied and deleted)

**One-time Charges:**
- Bedrock API calls - Based on usage during workshop
- Data transfer costs - Minimal
- SES emails sent - Negligible cost

{{% notice tip %}}
Monitor your AWS Cost Explorer for 2-3 days after cleanup to ensure no unexpected charges appear.
{{% /notice %}}

### Troubleshooting Cleanup Issues

**Issue: CDK destroy fails**
- Check CloudFormation console for specific error messages
- Manually delete stuck resources through AWS Console
- Retry `cdk destroy` after manual intervention

**Issue: RDS instance not deleting**
- Check if deletion protection is enabled
- Disable in RDS Console → Modify → uncheck "Enable deletion protection"
- Create final snapshot or skip if not needed

**Issue: Still seeing charges**
- Check for resources in other regions (this workshop uses ap-northeast-1)
- Look for CloudWatch Logs log groups (can accumulate storage costs)
- Review Cost Explorer for detailed breakdown



Congratulations! You've successfully cleaned up all workshop resources. Thank you for completing this workshop!
