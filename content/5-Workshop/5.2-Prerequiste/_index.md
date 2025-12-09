---
title : "Prerequisite"
date :  "2025-09-09" 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

# MeetAssist text-to-SQL chatbot using Amazon Bedrock, Amazon DynamoDB, and Amazon RDS

To manually create a virtualenv on macOS and Linux:

```
$ python3 -m venv .venv
```

After the init process completes and the virtualenv is created, you can use the following
step to activate your virtualenv.

```
$ source .venv/bin/activate
```

If you are a Windows platform, you would activate the virtualenv like this:

```
% .venv\Scripts\activate.bat
```

Once the virtualenv is activated, you can install the required dependencies.

```
$ pip install -r requirements.txt
```

## Prerequisites

The following are needed in order to proceed with this post:

* An [AWS account](https://aws.amazon.com/).
* A [Facebook account](https://www.facebook.com/) connected to [Facebook Developers](https://developers.facebook.com/) for creating the Messenger chatbot.
* A [Facebook Page](https://www.facebook.com/pages/creation/) that will be used to host the chatbot (create a new page or use an existing one).
* A [Git client](https://git-scm.com/downloads) to clone the source code provided.
* [Docker](https://www.docker.com/) installed and running on the local host or laptop.
* [Install AWS CDK](https://docs.aws.amazon.com/cdk/v2/guide/getting-started.html)
* The [AWS Command Line Interface (AWS CLI)](https://aws.amazon.com/cli/).
* The AWS Systems Manager [Session Manager plugin](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html).
* [Amazon Bedrock model access](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html) enabled for Anthropic Claude 3.5 Sonnet, Claude 3 Sonnet, Claude 3 Haiku and Amazon Titan Embeddings G1 – Text in the ap-northeast-1 Region.
* Python 3.12 or higher with the pip package manager.
* Node.js (version 18.x or higher) and npm – required for running the dashboard, installing dependencies, and building workshop assets.