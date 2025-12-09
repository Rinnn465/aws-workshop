---
title : "Prepare Data"
date :  "2025-09-09" 
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Download the Dataset and Upload to Amazon S3

### Step 1: Download the Dataset

1. Navigate to the [MeetAssistData](https://drive.google.com/drive/folders/1JQ9X9BbKL7q82sEifvN5Seas7Mrgh4Q7?usp=sharing)
2. Download the data to your local machine
3. Unzip the file, which will expand into a folder called `DATA`

{{% notice warning %}}
**IMPORTANT - Do NOT open CSV files with Excel:**
- **Microsoft Excel can automatically convert data formats**, which may corrupt the data (e.g., phone numbers, dates, IDs may be altered)
- **Recommended approach:** Upload the data to S3 first (steps below), then use **VS Code to view/validate** the CSV files instead of Excel
- **If you must view locally:** Use **VS Code only** - it won't modify your data like Excel does
- **Keep original CSV files intact** before uploading to S3
{{% /notice %}}

### Step 2: Create S3 Bucket

Run this CLI script to create the Amazon S3 bucket. Replace `<account-id>` with your AWS account ID:

```bash
aws s3 mb s3://meetassist-data-<account-id>-ap-northeast-1 --region ap-northeast-1
```

{{% notice tip %}}
To find your AWS Account ID, run: `aws sts get-caller-identity --query Account --output text`
{{% /notice %}}


![S3 Bucket Creation](/images/5-Workshop/5.5-PrepareData/1.jpg)

### Step 3: Upload Data to S3

1. Go to the AWS S3 Console
2. Navigate to the bucket you just created: `meetassist-data-<account-id>-ap-northeast-1`
3. Create a folder named **`data`**
4. Upload all CSV files from the unzipped `DATA` folder into the `data` folder in S3


![data folder](/images/5-Workshop/5.5-PrepareData/2.jpg)

![upload files](/images/5-Workshop/5.5-PrepareData/3.jpg)

### Verification

After uploading, verify that all CSV files are present in your S3 bucket under the `data/` prefix:

```bash
aws s3 ls s3://meetassist-data-<account-id>-ap-northeast-1/data/
```

You should see all the CSV files listed in the output.
