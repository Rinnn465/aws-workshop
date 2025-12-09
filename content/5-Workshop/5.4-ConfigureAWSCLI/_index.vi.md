---
title : "Cấu hình AWS CLI"
date :  "2025-09-09" 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Cấu hình AWS CLI

Để triển khai và quản lý giải pháp, bạn cần cấu hình AWS Command Line Interface (AWS CLI) với thông tin xác thực của mình.

### Các bước

1. Gõ `aws configure` trong terminal của bạn. Đảm bảo bạn đã tạo khóa truy cập bí mật CLI cho tài khoản của mình (khuyến nghị sử dụng tài khoản IAM có quyền admin)

2. Hoàn thành biểu mẫu cấu hình:
   - **AWS Access Key ID**: Khóa truy cập của bạn
   - **AWS Secret Access Key**: Khóa bí mật của bạn
   - **Default region name**: `ap-northeast-1`
   - **Default output format**: `json`

### Tạo IAM Access Keys

{{% notice info %}}
Để tạo khóa truy cập IAM, thực hiện các bước sau:
1. Truy cập AWS Console → IAM → Users → Your User
2. Chuyển đến tab **Security Credentials**
3. Nhấp **Create Access Key**
4. Tải xuống hoặc lưu thông tin xác thực của bạn một cách an toàn
{{% /notice %}}

{{% notice warning %}}
Không bao giờ chia sẻ khóa truy cập AWS của bạn hoặc commit chúng vào version control. Lưu trữ chúng một cách an toàn và xoay vòng chúng thường xuyên.
{{% /notice %}}

### Xác minh

Sau khi cấu hình, xác minh cài đặt của bạn bằng cách chạy:

```bash
aws sts get-caller-identity
```

Bạn sẽ thấy ID tài khoản, ARN người dùng và ID người dùng của mình trong phản hồi.
