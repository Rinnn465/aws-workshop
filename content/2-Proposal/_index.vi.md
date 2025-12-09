---
title: "Bản đề xuất"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Chatbot Lên Lịch Thông Minh trên AWS
## Giải pháp Serverless Tự động hóa Đặt lịch & Hỗ trợ
[![Download MeetAssist Chatbot Proposal](https://img.shields.io/badge/MeetAssist_Chatbot_Proposal-Click_Here-0056D2?style=for-the-badge&logo=google-docs&logoColor=white)](/images/2-Proposal/Proposal_Template.docx)

### 1. Tóm tắt Dự án (Executive Summary)
Chatbot Lên Lịch Thông Minh trên AWS là một giải pháp hoàn toàn không máy chủ (serverless) được thiết kế để tự động hóa việc đặt lịch hẹn và hỗ trợ khách hàng qua Facebook Messenger. Hệ thống tích hợp các Mô hình Ngôn ngữ Lớn (LLMs) trên Amazon Bedrock (Claude 3.5 Sonnet, Claude 3 Haiku, Claude 3 Sonnet) sử dụng cơ chế Text-to-SQL để truy vấn/thực thi SQL trên cơ sở dữ liệu PostgreSQL. Giải pháp đảm bảo phản hồi chính xác theo ngữ cảnh, giảm 80–90% khối lượng công việc lên lịch thủ công trong khi vẫn duy trì bảo mật cấp doanh nghiệp tại khu vực Châu Á Thái Bình Dương (Tokyo).

### 2. Vấn đề & Giải pháp
### Vấn đề là gì?
Việc lên lịch hẹn thủ công tạo ra khối lượng công việc lớn đối với nhân viên, dẫn đến kém hiệu quả và chậm trễ trong phản hồi. Thiếu khả năng xử lý tự động cho các truy vấn phức tạp (ví dụ: kiểm tra khung giờ trống cụ thể hoặc sửa đổi lịch đặt), và các kênh hỗ trợ hiện tại thường gặp lỗi do con người hoặc không khả dụng ngoài giờ hành chính.

### Giải pháp
Nền tảng sử dụng **Amazon Bedrock** để tận dụng các Mô hình Nền tảng (Gia đình Claude 3) cho việc nhận diện ý định và tạo Text-to-SQL. **AWS Lambda** và **Amazon API Gateway** xử lý logic nghiệp vụ và tích hợp Facebook Webhook. **Amazon RDS (PostgreSQL)** lưu trữ dữ liệu lịch hẹn có cấu trúc, trong khi **Amazon DynamoDB** quản lý ngữ cảnh phiên làm việc. **Amazon SES** cung cấp xác thực OTP bảo mật. Hệ thống cung cấp một Admin Dashboard được lưu trữ trên **Amazon S3** và **CloudFront** để các tư vấn viên quản lý lịch trình hiệu quả.

### Lợi ích và Tỷ suất Hoàn vốn (ROI)
Giải pháp giúp giảm **80–90%** khối lượng công việc lên lịch thủ công và duy trì thời gian phản hồi toàn trình dưới 5 giây. Hệ thống cung cấp **thời gian hoạt động (uptime) 99.9%** thông qua kiến trúc serverless và đảm bảo bảo mật dữ liệu nghiêm ngặt qua việc cô lập VPC và xác thực Cognito. Chi phí hàng tháng ước tính là **$37.24 USD**, cung cấp mô hình thanh toán theo mức sử dụng (pay-as-you-go) hiệu quả về chi phí, có khả năng mở rộng theo lưu lượng truy cập, loại bỏ nhu cầu về hạ tầng máy chủ cố định đắt đỏ.

### 3. Kiến trúc Giải pháp
Nền tảng áp dụng kiến trúc **Serverless-First** và **Hướng sự kiện (Event-Driven)** được lưu trữ tại vùng ap-northeast-1. Tin nhắn gửi đến được đẩy vào hàng đợi Amazon SQS trước khi các hàm Lambda xử lý. Lambda tương tác với Amazon Bedrock để suy luận AI và với RDS để lưu trữ dữ liệu. Kiến trúc được chi tiết dưới đây:

![Kiến trúc Chatbot](/images/2-Proposal/chatbot_final_final_final.drawio.png)

### Các Dịch vụ AWS Sử dụng
- **Amazon Bedrock**: Truy cập Claude 3 Haiku (Ý định), Claude 3 Sonnet (Ngữ cảnh), và Claude 3.5 Sonnet (Text2SQL).
- **AWS Lambda**: Xử lý ChatHandler, logic Text2SQL, và xử lý Webhook.
- **Amazon API Gateway**: Điểm nhập an toàn cho Facebook Webhook và API Dashboard.
- **Amazon RDS (PostgreSQL)**: Lưu trữ tư vấn viên, khách hàng và dữ liệu lịch hẹn.
- **Amazon DynamoDB**: Quản lý phiên người dùng và cache ngữ cảnh hội thoại.
- **Amazon SQS (FIFO)**: Hàng đợi tin nhắn đến để xử lý bất đồng bộ.
- **Amazon SES**: Gửi email cho người dùng.
- **Amazon Cognito**: Quản lý xác thực cho Admin Dashboard.

### Thiết kế Thành phần
- **Lớp Giao diện (Frontend)**: Facebook Messenger qua Webhook và Admin Dashboard (React) trên S3/CloudFront.
- **Lớp Xử lý**: Lambda thực thi logic nghiệp vụ; SQS đảm bảo thứ tự tin nhắn; Bedrock xử lý suy luận AI.
- **Lớp Dữ liệu**: RDS cho dữ liệu quan hệ (private subnet); DynamoDB cho truy xuất phiên tốc độ cao.
- **Bảo mật**: VPC Endpoints cho giao tiếp nội bộ; Secrets Manager cho thông tin xác thực; thực thi IAM least privilege.
- **Quản lý Người dùng**: Amazon Cognito cho nhân viên; Chữ ký HMAC Facebook Messenger cho người dùng cuối.

### 4. Triển khai Kỹ thuật
**Các Giai đoạn Triển khai**
Dự án này tuân theo phương pháp Agile Scrum chia thành 4 giai đoạn chính:
- **Học tập & Thực hành Lab AWS**: Tập trung vào kiến thức cơ bản về Serverless (Lambda, API Gateway, RDS) và bảo mật IAM (Tháng 9 – Tháng 10).
- **Nghiên cứu & Phát triển**: Hoàn thiện kiến trúc Text-to-SQL, chọn mô hình Bedrock, và thiết kế schema SQL (Đầu tháng 11).
- **Phát triển Hệ thống Cốt lõi**: Xây dựng WebhookReceiver, ChatHandler, mô-đun Text-to-SQL, và tích hợp Amazon Bedrock (Giữa – Cuối tháng 11).
- **Hạ tầng & Dashboard**: Triển khai VPC/Hạ tầng qua CDK, phát triển Admin Dashboard, và thực hiện kiểm thử toàn trình (Cuối tháng 11 – Tháng 12).

**Yêu cầu Kỹ thuật**
- **Công nghệ Cốt lõi**: Python 3.12 (Backend), TypeScript/React (Frontend), AWS CDK v2 (IaC).
- **Yêu cầu AI/ML**: Truy cập Anthropic Claude 3 Haiku, Claude 3.5 Sonnet, Claude 3 Sonnet và Amazon Titan Embeddings G1 qua Amazon Bedrock.
- **Cơ sở dữ liệu**: PostgreSQL với extension `unaccent` để hỗ trợ tiếng Việt; nhập dữ liệu CSV để khởi tạo.
- **Phụ thuộc bên ngoài**: Tài khoản Meta (Facebook) Developer cho Graph API v18.0; Định danh Amazon SES đã xác minh.

### 5. Dòng thời gian & Các cột mốc
**Lịch trình Dự án**
- **Tháng 9 – Tháng 10**: Học tập AWS & Các bài Lab thực hành.
- **Đầu tháng 11**: Thiết kế Kiến trúc & Lựa chọn Công nghệ.
- **Giữa tháng 11**: Phát triển Backend Cốt lõi (ChatHandler, Module SQL).
- **Cuối tháng 11**: Triển khai Hạ tầng & Frontend Admin Dashboard.
- **Tháng 12**: Kiểm thử Tích hợp, Tối ưu hóa và Thuyết trình Cuối kỳ.

### 6. Ước tính Ngân sách
Bạn có thể xem chi tiết ước tính ngân sách trên [Công cụ Tính giá AWS (AWS Pricing Calculator)](https://calculator.aws/#/estimate?id=ee545a5e20d05d16fbf6eab1e4e66a35b70a2323).

### Chi phí Hạ tầng
- **Dịch vụ AWS:**
    - **Amazon VPC**: $20.45/tháng (2 Interface Endpoints để bảo mật).
    - **Amazon Bedrock**: $9.08/tháng (Token cho các mô hình Claude 3 Haiku/Sonnet và Claude 3.5 Sonnent).
    - **Amazon RDS**: $5.83/tháng (db.t3.micro, 20GB lưu trữ).
    - **Amazon Cognito**: $0.50/tháng (10 người dùng hoạt động hàng tháng - MAU).
    - **Amazon SQS**: $0.50/tháng (1 triệu yêu cầu).
    - **AWS Secrets Manager**: $0.40/tháng.
    - **Amazon DynamoDB**: $0.28/tháng (On-demand).
    - **Amazon SES & S3**: <$0.10/tháng.
    - **API Gateway, Lambda, EventBridge**: $0.00 (Được bao gồm trong Free Tier).

**Tổng chi phí**: $37.24 mỗi tháng, tương đương khoảng $446.88 mỗi năm.

### 7. Đánh giá Rủi ro
#### Ma trận Rủi ro
- **Độ chính xác LLM (Ảo giác AI)**: Tác động trung bình, xác suất trung bình.
- **Biến động Chi phí**: Tác động thấp, xác suất trung bình (Biến động do Pay-as-you-go).
- **Quyền riêng tư Dữ liệu**: Tác động cao, xác suất thấp.
- **Lỗi tạo SQL**: Tác động cao, xác suất trung bình.
- **Thiếu ngữ cảnh (Nhận thức Ngữ cảnh)**: Tác động cao, xác suất thấp.
- **Tấn công Brute-force OTP**: Tác động cao nhưng xác suất thấp.

#### Chiến lược Giảm thiểu
- **Độ chính xác**: Kỹ thuật prompt chặt chẽ và các rào chắn phân quyền người dùng cơ sở dữ liệu (chỉ SELECT/INSERT).
- **Chi phí**: Tối ưu hóa VPC Endpoint (gỡ bỏ khi không dùng) và tận dụng Free Tier.
- **Quyền riêng tư**: Cơ sở dữ liệu nằm trong Subnet Riêng biệt Cô lập (Private Isolated Subnets); tuân thủ quản trị PII.
- **Tạo SQL**: Kiểm tra prompt được thực hiện nghiêm ngặt để xử lý các ràng buộc enum, xác minh tên cột/bảng, và định dạng đúng các mệnh đề `WHERE` (bao gồm toán tử `LIKE`) cho tên/văn bản tiếng Việt.
- **Ngữ cảnh**: System prompt sử dụng cơ chế gọi hàm bắt buộc để lấy thêm ngữ cảnh phiên làm việc, giúp LLM nắm bắt đầy đủ lịch sử trao đổi trước khi phản hồi.
- **Bảo mật OTP**: Áp dụng giới hạn tốc độ (tối đa 5 lần thử/phiên, thời gian hồi 15 giây), tự động chặn trong 3600 giây sau khi thất bại. OTP hết hạn sau 5 phút và xác minh sử dụng các phương pháp an toàn chống tấn công thời gian (HMAC timing-attack safe).

### 8. Kết quả Mong đợi
#### Cải tiến Kỹ thuật:
Tự động hóa việc đặt lịch dựa trên ngữ cảnh bằng cơ chế tạo SQL.
Độ trễ phản hồi toàn trình ≤ 5 giây.
Hạ tầng bảo mật, cô lập trong VPC với thời gian hoạt động (uptime) 99.9%.

#### Giá trị Dài hạn
Nền tảng có khả năng mở rộng để phát triển đa kênh (Web/Mobile).
Thu thập dữ liệu cho phân tích nâng cao trong tương lai (AWS Glue/Athena).
Tối ưu vận hành thông qua việc giảm thiểu công việc quản trị thủ công.