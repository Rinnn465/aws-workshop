---
title : "Dọn dẹp Tài nguyên"
date :  "2025-09-09" 
weight : 12
chapter : false
pre : " <b> 5.12. </b> "
---

## Dọn dẹp Tài nguyên

Để tránh phát sinh chi phí AWS không cần thiết, hãy làm theo các bước sau để xóa hoàn toàn tất cả tài nguyên được tạo trong workshop này.

{{% notice warning %}}
Quá trình dọn dẹp này là **không thể đảo ngược**. Tất cả dữ liệu, bao gồm thông tin khách hàng, lịch hẹn và hồ sơ tư vấn viên sẽ bị xóa vĩnh viễn. Đảm bảo xuất bất kỳ dữ liệu nào bạn cần trước khi tiếp tục.
{{% /notice %}}

### Bước 1: Hủy CDK Stack

Điều hướng đến thư mục dự án và hủy CDK stack:

```bash
cd MeetAssist
cdk destroy --all
```

Khi được nhắc, xác nhận xóa bằng cách gõ `y`.

Điều này sẽ xóa:
- Lambda functions
- API Gateway
- RDS PostgreSQL database
- DynamoDB tables
- Cognito User Pools
- S3 buckets (ngoại trừ những bucket có versioning/retention)
- CloudFront distributions
- SQS queues
- EventBridge rules
- IAM roles và policies

{{% notice info %}}
Quá trình CDK destroy có thể mất 30-40 phút để hoàn thành. Đợi xác nhận trước khi tiếp tục bước tiếp theo.
{{% /notice %}}

### Bước 2: Xóa S3 Buckets

Một số S3 bucket có thể không tự động xóa nếu chúng chứa objects. Xóa thủ công:

**Liệt kê các bucket:**
```bash
aws s3 ls | grep meetassist
```

**Làm trống và xóa từng bucket:**
```bash
aws s3 rm s3://meetassist-data-<account-id>-ap-northeast-1 --recursive
aws s3 rb s3://meetassist-data-<account-id>-ap-northeast-1

aws s3 rm s3://meetassist-dashboard-<account-id>-ap-northeast-1 --recursive
aws s3 rb s3://meetassist-dashboard-<account-id>-ap-northeast-1
```

Thay thế `<account-id>` bằng AWS account ID thực tế của bạn.

### Bước 3: Xóa Cognito Users

Nếu bạn tạo thủ công bất kỳ Cognito user nào không bị xóa:

```bash
aws cognito-idp list-users --user-pool-id <your-user-pool-id> --region ap-northeast-1
```

CDK destroy nên đã xóa User Pool, nhưng hãy xác minh trong console không còn tài nguyên mồ côi nào.

### Bước 4: Xóa Secrets Manager Secrets

Kiểm tra các secret còn lại:

```bash
aws secretsmanager list-secrets --region ap-northeast-1 | grep meetassist
```

Xóa bất kỳ secret nào tìm thấy:

```bash
aws secretsmanager delete-secret --secret-id MeetAssist/Facebook/PageAccessToken --region ap-northeast-1 --force-delete-without-recovery
aws secretsmanager delete-secret --secret-id MeetAssist/Facebook/VerifyToken --region ap-northeast-1 --force-delete-without-recovery
```

### Bước 5: Xóa SSM Parameters

Xóa Facebook App ID và App Secret:

```bash
aws ssm delete-parameter --name /MeetAssist/Facebook/AppId --region ap-northeast-1
aws ssm delete-parameter --name /MeetAssist/Facebook/AppSecret --region ap-northeast-1
```

### Bước 6: Xóa Facebook App Configuration

1. Truy cập [Facebook Developers](https://developers.facebook.com/)
2. Điều hướng đến app MeetAssist của bạn
3. Vào **Settings** → **Basic**
4. Cuộn xuống và nhấp **Delete App**
5. Xác nhận xóa

{{% notice tip %}}
Hoặc bạn có thể giữ Facebook App nhưng xóa webhook subscription và kết nối trang nếu bạn dự định xây dựng lại dự án sau này.
{{% /notice %}}

### Bước 7: Vô hiệu hóa Bedrock Models (Tùy chọn)

Nếu bạn không còn cần truy cập các Bedrock models:

1. Vào AWS Console → **Amazon Bedrock**
2. Điều hướng đến **Model access** trong thanh bên trái
3. Với mỗi model đã bật:
   - Claude 3.5 Sonnet
   - Claude 3 Sonnet
   - Claude 3 Haiku
   - Titan Embeddings G1 - Text
4. Nhấp **Manage** → **Disable access**

{{% notice info %}}
Quyền truy cập Bedrock model tự nó không phát sinh chi phí. Bạn chỉ bị tính phí cho các API call. Bạn có thể để các model được bật nếu dự định sử dụng chúng trong các dự án khác.
{{% /notice %}}

### Bước 8: Xác minh Dọn dẹp

Kiểm tra kỹ xem tất cả tài nguyên đã bị xóa:

**Kiểm tra CloudFormation Stacks:**
```bash
aws cloudformation list-stacks --region ap-northeast-1 | grep MeetAssist
```

**Kiểm tra Lambda Functions:**
```bash
aws lambda list-functions --region ap-northeast-1 | grep MeetAssist
```

**Kiểm tra RDS Instances:**
```bash
aws rds describe-db-instances --region ap-northeast-1 | grep meetassist
```

**Kiểm tra DynamoDB Tables:**
```bash
aws dynamodb list-tables --region ap-northeast-1 | grep MeetAssist
```

Tất cả lệnh nên trả về kết quả trống.

### Cân nhắc Chi phí

Sau khi dọn dẹp, bạn nên thấy những điều sau trong AWS billing:

**Chi phí Liên tục (Không có):**
- Lambda, API Gateway, RDS, DynamoDB - **$0** (tài nguyên đã xóa)
- CloudFront - **$0** (distribution đã xóa)
- S3 storage - **$0** (buckets đã làm trống và xóa)

**Chi phí Một lần:**
- Bedrock API calls - Dựa trên việc sử dụng trong workshop
- Data transfer costs - Tối thiểu
- SES emails sent - Chi phí không đáng kể

{{% notice tip %}}
Theo dõi AWS Cost Explorer của bạn trong 2-3 ngày sau khi dọn dẹp để đảm bảo không có chi phí bất ngờ nào xuất hiện.
{{% /notice %}}

### Xử lý Sự cố Dọn dẹp

**Vấn đề: CDK destroy thất bại**
- Kiểm tra CloudFormation console để tìm thông báo lỗi cụ thể
- Xóa thủ công các tài nguyên bị kẹt qua AWS Console
- Thử lại `cdk destroy` sau can thiệp thủ công


**Vấn đề: RDS instance không xóa**
- Kiểm tra xem deletion protection có được bật không
- Vô hiệu hóa trong RDS Console → Modify → bỏ chọn "Enable deletion protection"
- Tạo final snapshot hoặc bỏ qua nếu không cần

**Vấn đề: Vẫn thấy chi phí**
- Kiểm tra tài nguyên ở các region khác (workshop này sử dụng ap-northeast-1)
- Tìm CloudWatch Logs log groups (có thể tích lũy chi phí lưu trữ)
- Xem lại Cost Explorer để phân tích chi tiết



Chúc mừng! Bạn đã dọn dẹp thành công tất cả tài nguyên workshop. Cảm ơn bạn đã hoàn thành workshop này!
