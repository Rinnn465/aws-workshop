---
title : "Thiết lập Messenger Bot"
date :  "2025-09-09" 
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

## Thiết lập Messenger Chatbot

MeetAssist chatbot được tích hợp với Facebook Messenger, cho phép người dùng tương tác tự nhiên để đặt, cập nhật hoặc hủy lịch hẹn.

### Bước 1: Tạo Facebook App

1. Truy cập [Facebook Developers](https://developers.facebook.com/)
2. Nhấp **"My Apps"** 

![Create App](/images/5-Workshop/5.7-SetupMessengerBot/1.png)

3. Chọn **"Create an app"**

![App Details](/images/5-Workshop/5.7-SetupMessengerBot/2.png)

4. Điền tên app của bạn (ví dụ: `demo`) và App Contact Email → Nhấp **"Next"**

![Business Profile](/images/5-Workshop/5.7-SetupMessengerBot/4.png)

5. Chọn **"Messaging businesses"** làm use case → Nhấp **"Receive"

![App Settings](/images/5-Workshop/5.7-SetupMessengerBot/5.png)

6. Chọn hồ sơ **"Business"** của bạn hoặc chọn none nếu bạn chỉ muốn test app → Nhấp **"Receive"**

![Privacy Policy](/images/5-Workshop/5.7-SetupMessengerBot/6.png)
![Use Cases](/images/5-Workshop/5.7-SetupMessengerBot/7.png)

7. Nhấp **"Go to Dashboard"**

![Messenger Settings](/images/5-Workshop/5.7-SetupMessengerBot/8.png)

### Bước 2: Cấu hình App Settings

1. Trong app dashboard, nhấp **"App Settings"** → **"Basic info"**

![Page Access Token](/images/5-Workshop/5.7-SetupMessengerBot/9.png)

2. Sao chép và lưu **App ID** và **App Secret** của bạn

![AppID-Apsecret](/images/5-Workshop/5.7-SetupMessengerBot/10.png)

3. Dán Privacy Policy URL: `https://www.freeprivacypolicy.com/live/e7193dae-4bba-4482-876e-7b76d83a0676`

![Privacy Policy URL](/images/5-Workshop/5.7-SetupMessengerBot/11.png)

4. Chọn **"Messenger for Business"** làm app category → Nhấp **"Save Changes"**

![App Category](/images/5-Workshop/5.7-SetupMessengerBot/12.png)



### Bước 3: Lưu trữ Thông tin xác thực Facebook trong AWS

Chạy các lệnh AWS CLI sau để lưu trữ an toàn thông tin xác thực Facebook của bạn:

#### Tạo SSM Parameters:

```powershell
# Facebook App ID
aws ssm put-parameter `
    --name "/meetassist/facebook/app_id" `
    --value "YOUR_FACEBOOK_APP_ID" `
    --type "String" `
    --description "Facebook App ID for MeetAssist" `
    --region ap-northeast-1

# Facebook App Secret
aws ssm put-parameter `
    --name "/meetassist/facebook/app_secret" `
    --value "YOUR_FACEBOOK_APP_SECRET" `
    --type "String" `
    --description "Facebook App Secret for MeetAssist" `
    --region ap-northeast-1
```

#### Tạo Secrets Manager Secrets:

```powershell
# Facebook Page Access Token (lấy từ bước 4 bên dưới)
aws secretsmanager create-secret `
    --name "meetassist/facebook/page_token" `
    --description "Facebook Page Access Token for MeetAssist" `
    --secret-string "YOUR_FACEBOOK_PAGE_ACCESS_TOKEN" `
    --region ap-northeast-1

# Facebook Verify Token (tạo một chuỗi ngẫu nhiên, ví dụ: "my_secure_token_12345")
aws secretsmanager create-secret `
    --name "/meetassist/facebook/verify_token" `
    --description "Facebook Webhook Verify Token for MeetAssist" `
    --secret-string "YOUR_CUSTOM_VERIFY_TOKEN_123456" `
    --region ap-northeast-1
```

{{% notice warning %}}
Thay thế `YOUR_FACEBOOK_APP_ID`, `YOUR_FACEBOOK_APP_SECRET`, `YOUR_FACEBOOK_PAGE_ACCESS_TOKEN`, và `YOUR_CUSTOM_VERIFY_TOKEN_123456` bằng các giá trị thực tế của bạn.
{{% /notice %}}

### Bước 4: Kết nối Facebook Page và Lấy Page Access Token

1. Trong app dashboard, nhấp **"Use Cases"** → **"Customize"**

![Use Cases](/images/5-Workshop/5.7-SetupMessengerBot/13.png)

2. Đi đến **"Install the Messenger API"**, nhấp **"Connect"** để liên kết Facebook Page của bạn với app

![Messenger API](/images/5-Workshop/5.7-SetupMessengerBot/14.png)

3. Chọn **"Create"** để sao chép **Page Access Token** được tạo

![Page Access Token](/images/5-Workshop/5.7-SetupMessengerBot/15.png)

4. Sử dụng token này trong lệnh `aws secretsmanager create-secret` ở trên

### Bước 5: Cấu hình Webhooks API

1. Lấy Webhook URL của bạn từ file `outputs.json` (được tạo sau khi triển khai CDK)
2. Trong app dashboard, đi đến **"Messenger API Settings"**
3. Đi đến phần **"Configure Webhooks"**
4. Nhập thông tin sau:
   - **Callback URL**: `https://<your-api-gateway-url>/webhook` (từ `outputs.json`)
   - **Verify Token**: Cùng chuỗi ngẫu nhiên bạn đã sử dụng ở bước 3 (ví dụ: `YOUR_CUSTOM_VERIFY_TOKEN_123456`)

![Callback URL](/images/5-Workshop/5.7-SetupMessengerBot/16.png)

5. Nhấp **"Verify and Save"**
6. Subscribe các webhook fields sau:
   - `messages`
   - `messaging_postbacks`
   - `messaging_account_linking`

![Webhook Fields](/images/5-Workshop/5.7-SetupMessengerBot/17.png)


### Bước 7: Cấu hình Messenger Profile (Nút Get Started & Greeting)

Sau khi triển khai, chatbot tự động cấu hình:
- **Nút Get Started**: Người dùng nhấp vào để bắt đầu trò chuyện
- **Greeting Text**: Tin nhắn chào mừng hiển thị trước khi người dùng bắt đầu chat

Để cập nhật thủ công nếu cần:

```bash
# Đặt nút Get Started
curl -X POST "https://graph.facebook.com/v18.0/me/messenger_profile?access_token=<PAGE_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "get_started": {"payload": "GET_STARTED"}
  }'

# Đặt Greeting Text
curl -X POST "https://graph.facebook.com/v18.0/me/messenger_profile?access_token=<PAGE_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "greeting": [
      {
        "locale": "default",
        "text": "Xin chào! Mình là MeetAssist, trợ lý đặt lịch hẹn tư vấn hướng nghiệp. Hãy nhấn \"Bắt đầu\" để sử dụng dịch vụ! 👋"
      }
    ]
  }'
```

### Bước 8: Chế độ App và Quyền

{{% notice info %}}
**Development Mode**: App của bạn hiện đang ở chế độ development. Chỉ bạn (nhà phát triển app) và người test bạn thêm vào mới có thể tương tác với bot.

**Public Access**: Để cho phép người dùng khác sử dụng bot của bạn, đi đến app dashboard và chuyển app sang **"Live Mode"** bằng cách chọn **"Post"**

![Live Mode](/images/5-Workshop/5.7-SetupMessengerBot/18.png)

**App Review**: Để có đầy đủ tính năng và quyền, bạn phải hoàn thành quy trình App Review của Facebook. Chỉ để test thì không cần App Review.
{{% /notice %}}

### Xác minh

Kiểm tra bot của bạn bằng cách:
1. Mở Facebook Page của bạn trong Messenger
2. Nhấp nút **"Get Started"**
![Live Mode](/images/5-Workshop/5.7-SetupMessengerBot/19.png)
3. Xác minh bạn nhận được tin nhắn chào mừng
4. Thử gửi một tin nhắn test để xác nhận webhook hoạt động

Nếu mọi thứ được cấu hình đúng, bot sẽ phản hồi tin nhắn của bạn!
