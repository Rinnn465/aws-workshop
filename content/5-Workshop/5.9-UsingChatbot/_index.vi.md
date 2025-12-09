---
title : "Sử dụng Chatbot"
date :  "2025-09-09" 
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

## Sử dụng Chatbot

Chatbot MeetAssist có thể truy cập qua Facebook Messenger và cung cấp giao diện hội thoại để đặt lịch hẹn với các tư vấn viên.

### Bắt đầu

1. Mở Facebook Messenger và tìm kiếm trang đã kết nối của bạn
2. Nhấp vào nút **Get Started**
3. Chatbot sẽ chào hỏi và yêu cầu xác thực

![Live Mode](/images/5-Workshop/5.7-SetupMessengerBot/20.png)

### Luồng Xác thực

Trước khi sử dụng chatbot, bạn cần xác thực:

1. **Xác minh Email**: Nhập địa chỉ email đã đăng ký của bạn
2. **Yêu cầu OTP**: Bot sẽ gửi mã One-Time Password đến email của bạn
3. **Nhập OTP**: Nhập mã 6 chữ số từ email của bạn (kiểm tra trong phần spam)
4. **Phiên Hoạt động**: Phiên của bạn có hiệu lực trong 24 giờ
![Live Mode](/images/5-Workshop/5.7-SetupMessengerBot/21.png)
{{% notice warning %}}
Nếu AWS SES của bạn đang ở **chế độ sandbox**, bạn chỉ có thể gửi email đến các địa chỉ đã xác minh. Để sử dụng production, hãy yêu cầu quyền truy cập SES production.
{{% /notice %}}

### Đặt Lịch Hẹn

Chatbot sử dụng khả năng hiểu ngôn ngữ tự nhiên được hỗ trợ bởi Amazon Bedrock. Bạn có thể đặt lịch hẹn bằng tiếng Việt đàm thoại:

**Ví dụ hội thoại:**
- "Tôi muốn đặt lịch với tư vấn viên Nguyễn Văn A vào thứ 2 tuần sau lúc 10 giờ sáng"
- "Book appointment with consultant John next Monday at 2pm"
- "Đặt lịch gặp chuyên gia Trần Thị B ngày mai buổi chiều"

Chatbot sẽ:
1. Trích xuất thông tin lịch hẹn (tư vấn viên, ngày, giờ)
2. Kiểm tra lịch trống của tư vấn viên
3. Xác nhận đặt lịch với bạn
4. Tạo lịch hẹn trong hệ thống

### Cập nhật Lịch Hẹn

Để chỉnh sửa lịch hẹn hiện có:
- "Tôi muốn đổi lịch hẹn sang thứ 4"
- "Change my appointment to 3pm"
- "Reschedule my meeting with consultant A"

Chatbot sẽ hiển thị các lịch hẹn hiện tại của bạn và hướng dẫn bạn qua quy trình cập nhật.

### Hủy Lịch Hẹn

Để hủy lịch hẹn:
- "Hủy lịch hẹn của tôi"
- "Cancel my appointment"
- "I want to cancel my meeting"

Bot sẽ liệt kê các lịch hẹn đang hoạt động của bạn và yêu cầu xác nhận trước khi hủy.

### Truy vấn Chung

Hỏi chatbot về:

**Tư vấn viên:**
- "Có những tư vấn viên nào?"
- "Who are the available consultants?"
- "Tell me about consultant Nguyễn Văn A"

**Lịch Trống:**
- "Tư vấn viên A có lịch trống khi nào?"
- "Show me available slots for next week"
- "When is consultant B free?"

**Lịch Hẹn của Bạn:**
- "Lịch hẹn của tôi"
- "My appointments"
- "Show my upcoming meetings"

### Hủy Bỏ Thao Tác

Nếu bạn muốn hủy luồng hội thoại hiện tại:
- Gõ "abort" hoặc "hủy" bất cứ lúc nào
- Bot sẽ reset và bạn có thể bắt đầu yêu cầu mới

### Quản lý Phiên

- Phiên hết hạn sau **24 giờ**
- Bạn sẽ cần xác thực lại bằng email + OTP
- Lịch sử hội thoại của bạn được duy trì trong suốt phiên

### Xử lý Sự cố

**Vấn đề: Bot không phản hồi**
- Kiểm tra xem Facebook webhook đã được cấu hình đúng chưa
- Xác minh API Gateway URL trong cài đặt webhook
- Kiểm tra Lambda logs trong CloudWatch

**Vấn đề: Không nhận được OTP**
- Xác minh email của bạn là chính xác
- Kiểm tra thư mục spam/junk
- Nếu ở chế độ SES sandbox, đảm bảo email đã được xác minh trong SES Console

**Vấn đề: Đặt lịch hẹn thất bại**
- Đảm bảo tư vấn viên tồn tại trong database
- Kiểm tra xem khung giờ yêu cầu có sẵn không
- Xác minh định dạng ngày được bot hiểu

**Vấn đề: Bedrock model bị throttling**
- Nếu bạn thấy phản hồi chậm, có thể bạn đang chạm giới hạn tốc độ Bedrock
- Cân nhắc yêu cầu tăng quota trong Service Quotas console

{{% notice tip %}}
Chatbot học từ ngữ cảnh. Nếu nó không hiểu, hãy thử diễn đạt lại yêu cầu của bạn với chi tiết cụ thể hơn như ngày giờ chính xác.
{{% /notice %}}

Bây giờ bạn có thể bắt đầu tương tác với chatbot MeetAssist để quản lý lịch hẹn của mình!
