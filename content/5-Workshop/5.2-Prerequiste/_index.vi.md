---
title : "Các bước chuẩn bị"
date :  "2025-09-09" 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

# MeetAssist text-to-SQL chatbot sử dụng Amazon Bedrock, Amazon DynamoDB và Amazon RDS

Để tạo virtualenv thủ công trên macOS và Linux:

```
$ python3 -m venv .venv
```

Sau khi quá trình khởi tạo hoàn tất và virtualenv được tạo, bạn có thể sử dụng bước sau để kích hoạt virtualenv của mình.

```
$ source .venv/bin/activate
```

Nếu bạn sử dụng nền tảng Windows, bạn sẽ kích hoạt virtualenv như sau:

```
% .venv\Scripts\activate.bat
```

Sau khi virtualenv được kích hoạt, bạn có thể cài đặt các dependencies cần thiết.

```
$ pip install -r requirements.txt
```

## Yêu cầu Tiên quyết

Các yêu cầu sau cần có để tiếp tục với bài workshop này:

* Một [tài khoản AWS](https://aws.amazon.com/).
* Một [tài khoản Facebook](https://www.facebook.com/) được kết nối với [Facebook Developers](https://developers.facebook.com/) để tạo chatbot Messenger.
* Một [Facebook Page](https://www.facebook.com/pages/creation/) sẽ được sử dụng để lưu trữ chatbot (tạo trang mới hoặc sử dụng trang hiện có).
* Một [Git client](https://git-scm.com/downloads) để clone source code được cung cấp.
* [Docker](https://www.docker.com/) được cài đặt và chạy trên máy local hoặc laptop.
* [Cài đặt AWS CDK](https://docs.aws.amazon.com/cdk/v2/guide/getting-started.html)
* [AWS Command Line Interface (AWS CLI)](https://aws.amazon.com/cli/).
* AWS Systems Manager [Session Manager plugin](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html).
* [Quyền truy cập Amazon Bedrock model](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html) được bật cho Anthropic Claude 3.5 Sonnet, Claude 3 Sonnet, Claude 3 Haiku và Amazon Titan Embeddings G1 – Text trong Region ap-northeast-1.
* Python 3.12 hoặc cao hơn với trình quản lý gói pip.
* Node.js (phiên bản 18.x hoặc cao hơn) và npm – cần thiết để chạy dashboard, cài đặt dependencies và build các tài nguyên workshop.