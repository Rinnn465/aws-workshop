---
title : "Deploy the Solution"
date :  "2025-09-09" 
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

## Deploy the Solution

In this section, we will clone the MeetAssist repository and deploy the complete infrastructure using AWS CDK.

### Step 1: Clone the Repository

Clone the repository from GitHub:

```bash
git clone https://github.com/AWS-Vinhomes-Chatbot/MeetAssist
cd MeetAssist
```

### Step 2: Build the Dashboard

Before deploying the CDK application, we need to build the frontend dashboard.

#### Navigate to frontend folder

```bash
cd frontend
```

#### Install dependencies

Run the following command to install all necessary libraries:

```bash
npm i
```

#### Build the Dashboard

After the installation is complete, run the build command:

```bash
npm run build
```

Once the process completes, a `dist` directory will be created, containing the `index.html` file and the `assets` folder.

#### Return to project root

Use this command to return to the project's root folder:

```bash
cd ..
```

### Step 3: Deploy the CDK Application

Deploy the CDK application. It will take about **20-30 minutes** to deploy all of the resources.

```bash
cdk bootstrap aws://{{account_id}}/ap-northeast-1 
cdk deploy --all 
```

{{% notice note %}}
If you receive an error at this step, please ensure **Docker is running** on the local host or laptop.
{{% /notice %}}

{{% notice info %}}
Replace `{{account_id}}` with your actual AWS Account ID. You can find it by running:
```bash
aws sts get-caller-identity --query Account --output text
```
{{% /notice %}}

### Step 4: Initialize the Database with Embeddings

After the CDK deployment completes, you must run the **DataIndexer Lambda function** to populate the embeddings table with database schema information.

Use the following AWS CLI command:

```bash
aws lambda invoke \
  --function-name DataIndexerStack-DataIndexerFunction \
  --invocation-type Event \
  response.json \
  --region ap-northeast-1
```

{{% notice tip %}}
The DataIndexer function generates vector embeddings of your database schema, which enables the chatbot to understand and query your data using natural language.
{{% /notice %}}

### Step 5: Verify Deployment

After completing all the steps above, your environment is fully deployed and initialized. 

You can verify the deployment by checking:

1. **CloudFormation Stacks**: All stacks should show `CREATE_COMPLETE` status
2. **outputs.json file**: Contains important URLs and IDs for your deployment
3. **S3 Buckets**: Dashboard assets should be uploaded
4. **Lambda Functions**: All functions should be created and ready

### Next Steps

Now you can proceed to:
- Configure the Facebook Messenger integration (Section 5.7)
- Set up the Admin Dashboard (Section 5.8)
- Start using the MeetAssist chatbot (Section 5.9)
