---
title : "Setup Admin Dashboard"
date :  "2025-09-09" 
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

## Setup Admin Dashboard

The Admin Dashboard requires an administrator account created in Amazon Cognito. Follow these steps to access the dashboard for the first time.

### Step 1: Create an Admin User

Run the following AWS CLI command to create an admin account:

```bash
aws cognito-idp admin-create-user --user-pool-id <your-user-pool-id> --username <your-email> --user-attributes Name=email,Value=<your-email> Name=email_verified,Value=true --temporary-password "<your-temporary-password>" --region ap-northeast-1
```

{{% notice info %}}
Both the **User Pool ID** and the **Admin Dashboard URL** can be found in the `outputs.json` file generated after CDK deployment.
{{% /notice %}}

### Step 2: First Login

1. Open the Admin Dashboard URL from the `outputs.json` file
2. Log in with your email and temporary password
3. Cognito will prompt you to set a new permanent password
4. After updating your password, you will be redirected to the Admin Dashboard

### Step 3: Verify Access

After logging in, you should see the dashboard homepage with:
- System statistics (total customers, consultants, appointments)
- Appointments breakdown by status
- Recent appointments list

![Admin Dashboard Homepage](/images/5-Workshop/5.8-SetupAdminDashboard/1.jpg)

{{% notice tip %}}
You can create additional admin users by repeating Step 1 with different email addresses.
{{% /notice %}}

### Troubleshooting

**Issue: Cannot login**
- Verify the User Pool ID is correct
- Check if the user was created successfully in Cognito Console
- Ensure you're using the correct temporary password


Now you're ready to use the Admin Dashboard to manage consultants and appointments!
