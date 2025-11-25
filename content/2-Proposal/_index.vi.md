---
title: "Bản đề xuất"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---



# AI-Powered Booking Chatbot on AWS
## Giải pháp AWS Serverless ứng dụng LLM tích hợp RAG, SQL-Driven cho đặt lịch và chăm sóc khách hàng

### 1. Tóm tắt điều hành  
AI-Powered Booking Chatbot on AWS là giải pháp chatbot thông minh được thiết kế nhằm hỗ trợ người dùng trong việc đặt lịch và tra cứu thông tin dịch vụ thông qua Facebook Messenger. Hệ thống sử dụng LLM đưa ra quyết định kết hợp giữa cơ chế **RAG (Retrieval-Augmented Generation)** và **mô hình SQL-Driven** để vừa xử lý hội thoại tự nhiên, vừa truy xuất dữ liệu chính xác từ cơ sở dữ liệu PostgreSQL, DynamoDB.
Nền tảng sử dụng kiến trúc **AWS Serverless** giúp giảm thiểu chi phí vận hành, tự động mở rộng, và đảm bảo độ tin cậy.    

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Các mô hình chatbot hiện nay đa số chỉ dừng ở việc tư vấn các câu hỏi thông thường liên quan đến dịch vụ. Đặc biệt là việc đặt lịch vẫn thực hiện thủ công như nhắn tin hoặc gọi điện mà không tự động hoá hoàn toàn. Điều này khiến việc đặt lịch trở nên thiếu linh hoạt, hiệu quả kém, thiếu chính xác và tối ưu hoá khi số lượng người dùng tăng cao.
Việc triển khai chatbot AI có thể phức tạp nếu không có nền tảng đám mây linh hoạt để quản lý dữ liệu, luồng hội thoại, và bảo mật.


*Giải pháp*  
Dự án áp dụng AWS Lambda, API Gateway, DynamoDB, PostgreSQL, và các dịch vụ hỗ trợ AI để tạo nên chatbot đa năng có khả năng:
  - Được tích hợp vào Messenger có giao diện dễ dùng, dễ tiếp cận.
  - Phân tích intent hội thoại (đặt lịch, tư vấn, câu hỏi chung).
  - Kết nối cơ sở dữ liệu để truy xuất lịch, thông tin khách hàng, hoặc dữ liệu phân tích.
  - Hỗ trợ mô-đun RAG cho các câu hỏi mở hoặc ngữ cảnh phức tạp.
  - Cung cấp giao diện quản trị (Admin Dashboard) giúp theo dõi lịch sử hội thoại, thống kê và hiệu năng hệ thống.
 

*Lợi ích và hoàn vốn đầu tư (ROI)*  
Giải pháp này dự kiến tự động hóa **80-90%** quy trình đặt lịch, hoạt động 24/7 giúp tiết kiệm chi phí vận hành (so với hạ tầng on-premise) và chi phí nhân sự đồng thời tạo môi trường học tập thực tế cho sinh viên/nhóm nghiên cứu về AWS Serverless, NLP và RAG. Hệ thống có thể tái sử dụng và mở rộng để áp dụng cho các doanh nghiệp vừa và nhỏ trong tương lai.
  

### 3. Kiến trúc giải pháp  
**Mô tả tổng quan**:
Nền tảng hoạt động theo mô hình Serverless + VPC-secured, trong đó toàn bộ xử lý hội thoại, lịch đặt, và dữ liệu AI đều chạy trên AWS Lambda và dịch vụ không máy chủ

![Chatbot Architecture](/images/2-Proposal/chatbot_final_final.drawio.png)

*Luồng dữ liệu chính*
1. Người dùng trò chuyện qua Facebook Messenger → **API Gateway** → **Lambda WebhookReceiver** (xác minh, phân quyền).

2. **Lambda ChatOrchestrator** gọi Intent Model để xử lý intent, từ đó điều hướng tới SQL module hoặc RAG Module.

3. **DynamoDB** lưu cache hội thoại và metadata, trong khi **PostgreSQL** lưu lịch sử và thông tin đặt lịch.

4. **EventBridge** quản lý tác vụ chuyển dữ liệu đặt lịch định kỳ sau 1 ngày từ PostgreSQL lại về S3 để phục vụ cho Dashboard Admin


5. **Admin Dashboard** (Route 53 + Cloudfront + S3 + Cognito) giúp admin theo dõi, kiểm thử, phân tích dữ liệu và quản lý hệ thống một cách bảo mật.


*Dịch vụ AWS sử dụng*  
- *AWS Lambda*: Xử lý hội thoại, điều phối intent, lập lịch.

- *Amazon API Gateway*: Kết nối với Messenger và Admin Dashboard.

- *Amazon DynamoDB*:  Lưu cache, logs, metadata cho RAG, memory cho chatbot.
- *Amazon RDS (PostgreSQL)*: Lưu thông tin đặt lịch, lịch sử tương tác.

- *Amazon EventBridge*: Quản lý sự kiện, cron job.

- *Amazon S3 + CloudFront + Route 53*: Lưu trữ và phân phối giao diện quản trị.

- *Amazon Cognito*: Quản lý người dùng và phân quyền Admin.

- *AWS Secrets Manager*: Lưu trữ thông tin xác thực dịch vụ bảo mật.

- *AWS Glue + Athena* (phân tích tùy chọn): Trích xuất và phân tích dữ liệu lịch sử hội thoại.

- *Amazon Bedrock*: Phân tích Ý định (Intent) , trích xuất Thực thể (Entity) và sinh câu trả lời tự nhiên theo ngữ cảnh.
- *Amazon CloudWatch*: Trích xuất và phân tích dữ liệu logs trong hệ thống.


### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*  
Dự án gồm 2 phần — **xây dựng hệ thống chatbot và nền tảng quản trị AI Booking** — mỗi phần trải qua 4 giai đoạn chính:

1. *Nghiên cứu và thiết kế kiến trúc*  
   - Phân tích các mô hình chatbot tích hợp RAG (Retrieval-Augmented Generation) và intent classification.  
   - Đề xuất kiến trúc AWS Serverless phù hợp: Lambda, API Gateway, RDS PostgreSQL, DynamoDB, EventBridge.  
   - Đánh giá và lựa chọn Foundation Models trên Amazon Bedrock (Claude 3, Llama 2).
   - Nghiên cứu mô hình CI/CD với AWS CDK hoặc CloudFormation để triển khai tự động.  
   - (Thực hiện trước giai đoạn workshop — chuẩn bị môi trường kỹ thuật và sơ đồ kiến trúc.)

2. *Tính toán chi phí và kiểm tra tính khả thi*  
   - Sử dụng AWS Pricing Calculator để ước tính chi phí hạ tầng (Lambda, RDS, DynamoDB, Amplify, Cognito, EventBridge, S3, CloudFront).  
   - Thực hiện thử nghiệm nhỏ trên môi trường sandbox để kiểm chứng khả năng mở rộng, thời gian phản hồi và độ ổn định của chatbot.
   - (Giai đoạn đầu workshop — dùng kết quả để tinh chỉnh tài nguyên và định cỡ chi phí.)

3. *Điều chỉnh kiến trúc và tối ưu giải pháp*  
   - Cân đối chi phí và hiệu năng: tối ưu hóa số lượng Lambda, giảm chi phí cho mỗi lần chatbot thực hiện luồng tìm và trả lời câu hỏi, đặt lịch bằng việc áp dụng cơ chế caching bằng DynamoDB.  
   - Xây dựng cơ chế phân tách luồng hội thoại giữa intent “Booking” và “Customer Service” để giảm overhead xử lý và tiết kiệm chi phí cho LLM.
   - Kiểm thử khả năng mở rộng và tính ổn định khi tăng số lượng người dùng song song. 
   - (Giữa giai đoạn workshop — đảm bảo hệ thống đạt hiệu quả chi phí và kỹ thuật tối ưu.)

4. *Phát triển, kiểm thử và triển khai*  
   -  Phát triển các Lambda chính (WebhookReceiver, ChatOrchestrator, RAG Module, ScheduleExecutor, ArchiveData, Admin Manager), tích hợp RDS và DynamoDB. 
   - Cấu hình API Gateway, EventBridge và Cognito; xây dựng giao diện quản trị bằng JavaScript.  
   - Kiểm thử end-to-end: Messenger → API Gateway → Chatbot → Database → Dashboard.  
   - (Cuối workshop — đưa hệ thống vào vận hành, ghi nhận kết quả và demo hoàn chỉnh.)  

*Yêu cầu kỹ thuật*  
- Nền tảng chính: AWS Serverless (Lambda, API Gateway, DynamoDB, RDS PostgreSQL, EventBridge).  
- Bảo mật: Amazon Cognito, AWS Secrets Manager, IAM Role tách biệt.  
- Phát triển: AWS CDK/SDK, JavaScript cho giao diện quản trị.  
- Kết nối ngoài: Facebook Messenger Webhook (API Gateway endpoint).  
- Tự động hóa: CloudFormation template.

### 5. Lộ trình & Mốc triển khai   
- *Thực tập (Tháng 9–12)*:  
    - Tháng 9: Học AWS củng cố kiến trúc serverless, xây dựng prototype.
    - Tháng 10: Thiết kế và điều chỉnh kiến trúc.  
    - Tháng 11: Phát triển và kiểm thử hệ thống.
    - Tháng 12: Triển khai hoàn chỉnh, demo và đánh giá kết quả. 
- *Sau triển khai*: Nghiên cứu thêm trong vòng 1 năm.  

### 6. Ước tính ngân sách  

- Tải xuống báo cáo ước tính ngân sách (PDF): [Ước tính ngân sách - PDF](/images/2-Proposal/chatbotestimation.pdf).  



### Bảng chi phí (ước tính)

- Amazon Virtual Private Cloud (VPC): 57.04 USD — 6 VPC Interface endpoints mỗi khu vực AWS.
- Amazon Bedrock: 16.38 USD — 1 yêu cầu/phút, 8 giờ/ngày, 100 input token/yêu cầu, 50 output token/yêu cầu.
- AWS Web Application Firewall (WAF): 9.06 USD — 1 Web ACL, 3 Rules/Web ACL, 1 Managed Rule Group/Web ACL (hàng tháng).
- Amazon RDS for PostgreSQL: 7.87 USD — 1 node db.t3.micro (25% utilization/tháng), 20 GB (General Purpose SSD gp2), Single-AZ, On-Demand.
- Amazon EventBridge: 1.00 USD — 1 triệu custom events/tháng (payload 1 KB), 1 triệu invocations/tháng.
- Amazon DynamoDB: 0.96 USD — 1 GB dung lượng lưu trữ, 1 KB kích thước item trung bình, Table class: Standard.
- AWS Glue: 0.54 USD — 2 DPUs (Apache Spark), 0.0625 DPUs (Python Shell), 1 crawler.
- Amazon Athena: 0.45 USD — 30 queries/ngày, 0.1 GB dữ liệu quét/query.
- Amazon CloudFront: 0.24 USD — 1 GB data transfer out (internet)/tháng, 100,000 HTTPS requests/tháng.
- Amazon Simple Storage Service (S3): 0.13 USD — 5 GB S3 Standard storage/tháng.
- Amazon API Gateway: 0.13 USD — Ước tính 0.1 requests/tháng.
- AWS Lambda: 0.00 USD — 10,000 requests/tháng.
- Tổng cộng: 93.80 USD
  
  *Lưu ý quan trọng*: Các con số trên được tính toán dựa trên công cụ AWS Pricing Calculator và thể hiện mức ước tính ban đầu. Trong thực tế triển khai, chi phí này có khả năng sẽ thấp hơn. Điều này là do (1) việc sử dụng thực tế có thể không đạt đến mức tối đa như trong cấu hình ước tính, (2) khả năng tận dụng các gói miễn phí (Free Tier) của AWS, và (3) các tối ưu hóa chi phí (như caching, tinh chỉnh Lambda) sẽ được áp dụng trong quá trình vận hành.
 
### 7. Đánh giá rủi ro

| Rủi ro | Ảnh hưởng | Xác suất | Giảm thiểu |
|---|---:|---:|---|
| Messenger webhook gián đoạn | Trung bình | Trung bình | Thiết lập retry & log monitoring qua CloudWatch. |
| Sai phân quyền Lambda | Cao | Thấp | Sử dụng IAM Role riêng và kiểm thử quyền tối thiểu. |
| Tắc nghẽn dữ liệu DynamoDB | Trung bình | Thấp | Giới hạn TTL và cache cục bộ. |
| Vượt chi phí | Trung bình | Trung bình | Giám sát AWS Billing Alerts, bật Budget notification. |

### 8. Kết quả kỳ vọng  
- *Kỹ thuật*: Hoàn thiện chatbot AI có thể đặt lịch qua Messenger, tự động phản hồi câu hỏi khách hàng.
- *Học thuật*: Thành viên workshop hiểu quy trình thiết kế kiến trúc AWS Serverless có tích hợp RAG.
- *Thực tế*: Mở rộng mô hình thành chatbot doanh nghiệp, kết hợp phân tích dữ liệu hội thoại bằng Glue & Athena.
- *Giá trị dài hạn*: Tạo tiền đề cho nền tảng Customer Service AI nội bộ hoặc sản phẩm SaaS tương tự.