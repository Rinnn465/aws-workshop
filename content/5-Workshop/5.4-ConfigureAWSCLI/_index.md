---
title : "Configure AWS CLI"
date :  "2025-09-09" 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Configuration AWS CLI

To deploy and manage the solution, you need to configure the AWS Command Line Interface (AWS CLI) with your credentials.

### Steps

1. Type `aws configure` in your terminal. Make sure you have created CLI secret access key for your account (recommend using an IAM account with admin privileges)

2. Complete the configuration form:
   - **AWS Access Key ID**: Your access key
   - **AWS Secret Access Key**: Your secret key
   - **Default region name**: `ap-northeast-1`
   - **Default output format**: `json`

### Creating IAM Access Keys

{{% notice info %}}
To create IAM access keys, follow these steps:
1. Go to AWS Console → IAM → Users → Your User
2. Navigate to **Security Credentials** tab
3. Click **Create Access Key**
4. Download or save your credentials securely
{{% /notice %}}

{{% notice warning %}}
Never share your AWS access keys or commit them to version control. Store them securely and rotate them regularly.
{{% /notice %}}

### Verification

After configuration, verify your setup by running:

```bash
aws sts get-caller-identity
```

You should see your account ID, user ARN, and user ID in the response.
