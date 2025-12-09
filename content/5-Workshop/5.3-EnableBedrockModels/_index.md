---
title : "Enable Bedrock Models"
date :  "2025-09-09" 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Enabling Bedrock Models

Before deploying the solution, you need to enable the required Amazon Bedrock models in your AWS account.

### Steps to Enable Models

1. **Search for Amazon Bedrock** in AWS Console

![Amazon Bedrock Search](/images/5-Workshop/5.3-EnableBedrockModels/1.jpg)
2. **Access Model catalog** from the left navigation menu

![Model Catalog](/images/5-Workshop/5.3-EnableBedrockModels/2.jpg)
3. **Choose the corresponding model name:**
   - Anthropic Claude 3.5 Sonnet
   - Anthropic Claude 3 Sonnet
   - Anthropic Claude 3 Haiku
   - Amazon Titan Embeddings G1 – Text

![Model Selection](/images/5-Workshop/5.3-EnableBedrockModels/3.jpg)
4. **Select "Open in playground"** and send a test message to enable each model

![Open in Playground](/images/5-Workshop/5.3-EnableBedrockModels/4.jpg)

{{% notice note %}}
Make sure you enable all four models in the **ap-northeast-1 (Tokyo)** region as the solution is deployed in this region.
{{% /notice %}}


