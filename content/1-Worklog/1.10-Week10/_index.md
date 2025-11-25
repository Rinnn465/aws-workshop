---
title: "Week 10 Worklog"
date: "2025-09-09"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---



### Week 10 Objectives:

* Deploy admin dashboard interface for chatbot project.
* Deploy static website on AWS S3 and CloudFront.
* Integrate Route 53 and CloudFront to serve website.
* Research and prepare to integrate Amazon Cognito for admin login functionality.

### Tasks to carry out this week:
| Day | Tasks                                                                                                                                                                                   | Start date | Completion date | References                            |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Deploy first step of admin flow, design demo dashboard interface | 10/11/2025   | 10/11/2025      |
| 3   | - Push frontend code files to Amazon S3, test S3 static hosting <br> - Successfully deploy static web using S3 | 11/11/2025   | 11/11/2025      | [Amazon S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) |
| 4   | - Research CloudFront to integrate with previously deployed static web <br> - Configure CloudFront distribution to integrate with S3 static web | 12/11/2025   | 12/11/2025      | [Amazon CloudFront Documentation](https://docs.aws.amazon.com/cloudfront/) |
| 5   | - Successfully deploy static web on S3 via CloudFront and Route 53 | 13/11/2025   | 13/11/2025      | [CloudFront with S3](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GettingStarted.SimpleDistribution.html) |
| 6   | - Meeting to discuss and revise project architecture <br> - Remove Route 53 from architecture, use CloudFront domain directly <br> - Research to integrate admin login functionality using Cognito | 14/11/2025   | 14/11/2025      | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/) |


### Week 10 Achievements:

* Completed design of demo dashboard interface for admin flow.

* Successfully deployed static website hosting on Amazon S3:
  * Uploaded frontend code to S3 bucket
  * Configured S3 bucket for static website hosting
  * Tested and verified website works correctly

* Integrated CloudFront with S3 static website:
  * Created and configured CloudFront distribution
  * Connected CloudFront with S3 bucket
  * Optimized performance and caching

* Fully deployed static web via CloudFront and Route 53:
  * Configured DNS with Route 53
  * Connected domain with CloudFront distribution
  * Tested and verified entire flow

* Adjusted project architecture:
  * Decided to remove Route 53 from architecture
  * Use CloudFront domain directly to simplify
  * Updated and optimized architecture diagram

* Researched and prepared to integrate Amazon Cognito:
  * Learned about Cognito User Pool
  * Researched authentication flow for admin dashboard
  * Planned login functionality implementation
