---
title : "Using the Chatbot"
date :  "2025-09-09" 
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

## Using the Chatbot

The MeetAssist chatbot can be accessed via Facebook Messenger and provides a conversational interface for booking appointments with consultants.

### Getting Started

1. Open Facebook Messenger and search for your connected page
2. Click the **Get Started** button
3. The chatbot will greet you and request authentication

![Live Mode](/images/5-Workshop/5.7-SetupMessengerBot/20.png)

### Authentication Flow

Before using the chatbot, you need to authenticate:

1. **Email Verification**: Enter your registered email address
2. **OTP Request**: The bot will send a One-Time Password to your email
3. **Enter OTP**: Enter the 6-digit code from your email (check spam folder)
4. **Active Session**: Your session is valid for 24 hours

![Live Mode](/images/5-Workshop/5.7-SetupMessengerBot/21.png)
{{% notice warning %}}
If your AWS SES is in **sandbox mode**, you can only send emails to verified addresses. For production use, request SES production access.
{{% /notice %}}

### Booking an Appointment

The chatbot uses natural language understanding capabilities powered by Amazon Bedrock. You can book appointments using conversational Vietnamese:

**Example conversations:**
- "Tôi muốn đặt lịch với tư vấn viên Nguyễn Văn A vào thứ 2 tuần sau lúc 10 giờ sáng"
- "Book appointment with consultant John next Monday at 2pm"
- "Đặt lịch gặp chuyên gia Trần Thị B ngày mai buổi chiều"

The chatbot will:
1. Extract appointment information (consultant, date, time)
2. Check the consultant's available schedule
3. Confirm the booking with you
4. Create the appointment in the system

### Updating an Appointment

To edit an existing appointment:
- "Tôi muốn đổi lịch hẹn sang thứ 4"
- "Change my appointment to 3pm"
- "Reschedule my meeting with consultant A"

The chatbot will display your current appointments and guide you through the update process.

### Canceling an Appointment

To cancel an appointment:
- "Hủy lịch hẹn của tôi"
- "Cancel my appointment"
- "I want to cancel my meeting"

The bot will list your active appointments and request confirmation before canceling.

### General Queries

Ask the chatbot about:

**Consultants:**
- "Có những tư vấn viên nào?"
- "Who are the available consultants?"
- "Tell me about consultant Nguyễn Văn A"

**Available Schedule:**
- "Tư vấn viên A có lịch trống khi nào?"
- "Show me available slots for next week"
- "When is consultant B free?"

**Your Appointments:**
- "Lịch hẹn của tôi"
- "My appointments"
- "Show my upcoming meetings"

### Aborting Actions

If you want to cancel the current conversation flow:
- Type "abort" or "hủy" at any time
- The bot will reset and you can start a new request

### Session Management

- Sessions expire after **24 hours**
- You will need to re-authenticate with email + OTP
- Your conversation history is maintained throughout the session

### Troubleshooting

**Issue: Bot not responding**
- Check if the Facebook webhook is configured correctly
- Verify the API Gateway URL in webhook settings
- Check Lambda logs in CloudWatch

**Issue: Not receiving OTP**
- Verify your email is correct
- Check spam/junk folder
- If in SES sandbox mode, ensure the email is verified in SES Console

**Issue: Appointment booking fails**
- Ensure the consultant exists in the database
- Check if the requested time slot is available
- Verify the date format is understood by the bot

**Issue: Bedrock model throttling**
- If you see slow responses, you may be hitting Bedrock rate limits
- Consider requesting quota increases in Service Quotas console

{{% notice tip %}}
The chatbot learns from context. If it doesn't understand, try rephrasing your request with more specific details like exact dates and times.
{{% /notice %}}

Now you can start interacting with the MeetAssist chatbot to manage your appointments!
