---
title : "Thiết lập Admin Dashboard"
date :  "2025-09-09" 
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

## Thiết lập Admin Dashboard

Admin Dashboard yêu cầu một tài khoản quản trị viên được tạo trong Amazon Cognito. Thực hiện các bước sau để truy cập dashboard lần đầu tiên.

### Bước 1: Tạo Admin User

Chạy lệnh AWS CLI sau để tạo tài khoản admin:

```bash
aws cognito-idp admin-create-user --user-pool-id <your-user-pool-id> --username <your-email> --user-attributes Name=email,Value=<your-email> Name=email_verified,Value=true --temporary-password "<your-temporary-password>" --region ap-northeast-1
```

{{% notice info %}}
Cả **User Pool ID** và **Admin Dashboard URL** đều có thể tìm thấy trong file `outputs.json` được tạo sau khi triển khai CDK.
{{% /notice %}}

### Bước 2: Đăng nhập Lần đầu

1. Mở Admin Dashboard URL từ file `outputs.json`
2. Đăng nhập bằng email và mật khẩu tạm thời của bạn
3. Cognito sẽ yêu cầu bạn đặt mật khẩu vĩnh viễn mới
4. Sau khi cập nhật mật khẩu, bạn sẽ được chuyển hướng đến Admin Dashboard

### Bước 3: Xác minh Truy cập

Sau khi đăng nhập, bạn sẽ thấy trang chủ dashboard với:
- Thống kê hệ thống (tổng số khách hàng, tư vấn viên, lịch hẹn)
- Phân loại lịch hẹn theo trạng thái
- Danh sách lịch hẹn gần đây

![Admin Dashboard Home](/images/5-Workshop/5.8-SetupAdminDashboard/1.jpg)

{{% notice tip %}}
Bạn có thể tạo thêm admin user bằng cách lặp lại Bước 1 với các địa chỉ email khác nhau.
{{% /notice %}}

### Xử lý Sự cố

**Vấn đề: Không thể đăng nhập**
- Xác minh User Pool ID là chính xác
- Kiểm tra xem user đã được tạo thành công trong Cognito Console chưa
- Đảm bảo bạn đang sử dụng đúng mật khẩu tạm thời


Bây giờ bạn đã sẵn sàng sử dụng Admin Dashboard để quản lý tư vấn viên và lịch hẹn!
