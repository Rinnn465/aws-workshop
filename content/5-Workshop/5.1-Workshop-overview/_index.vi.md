---
title : "Giới thiệu"
date :  "2025-09-09" 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---


#### Tuyên bố vấn đề
Các hệ thống đặt lịch thủ công hoặc chatbot truyền thống thường gặp khó khăn khi lượng khách hàng tăng cao, dẫn đến trải nghiệm người dùng kém và tốn kém chi phí nhân sự trực page. Workshop này giải quyết vấn đề bằng cách xây dựng một kiến trúc có khả năng:
* **Tự động hóa:** Xử lý đặt, đổi, hủy lịch 24/7.
* **Hiểu ngữ cảnh:** Nhận diện ý định (Intent) của người dùng chính xác.
* **Truy xuất dữ liệu:** Trả lời các câu hỏi phức tạp về lịch trống, thông tin tư vấn viên.

#### Kiến trúc giải pháp
Hệ thống được thiết kế theo mô hình **Event-Driven Serverless** kết hợp với **VPC-secured** để đảm bảo bảo mật và khả năng mở rộng:

1.  **Frontend Interface:** Người dùng tương tác qua Facebook Messenger.
2.  **Request Handling:** 
    * Amazon API Gateway nhận Webhook từ Facebook.
    * AWS Lambda (WebhookReceiver) đẩy tin nhắn vào hàng đợi Amazon SQS (FIFO) để đảm bảo thứ tự và xử lý bất đồng bộ.
3.  **Brain (Processing Core):**
    * ChatHandler Lambda: Quản lý hội thoại, kiểm tra session từ Amazon DynamoDB.
    * Authentication: Xác thực người dùng qua Email OTP sử dụng Amazon SES.
4.  **AI & Data Layer:**
    * Amazon Bedrock: Sử dụng các mô hình Claude 3 Haiku (cho Intent Classification), Claude 3.5 Sonnet và Claude 3 Sonnet (cho Text-to-SQL & Extraction).
    * Amazon RDS (PostgreSQL): Lưu trữ dữ liệu nghiệp vụ (Lịch hẹn, Khách hàng, Tư vấn viên).
    * Text2SQL Handler: Chuyển đổi câu hỏi tự nhiên thành truy vấn SQL an toàn để lấy dữ liệu.
5.  **Admin Dashboard & Consultant Portal:** Giao diện quản trị (ReactJS) được host trên Amazon S3 và phân phối qua CloudFront, cho phép quản trị viên xem thống kê và quản lý lịch. Consultant Portal cung cấp khả năng quản lý lịch được book với khách hàng và xem lịch hẹn cá nhân.

![Architecture Diagram](/images/2-Proposal/chatbot_final_final_final.drawio.png)
*(Hình ảnh minh họa kiến trúc tổng quan từ Proposal)*

#### Key Technologies
Trong workshop này, bạn sẽ làm việc với các dịch vụ AWS chính sau:
+ **Amazon Bedrock**: Trái tim của AI, cung cấp các Foundation Models (Claude, Titan) để xử lý ngôn ngữ và sinh SQL.
+ **AWS Lambda & API Gateway**: Xây dựng backend serverless không cần quản lý máy chủ.
+ **Amazon RDS (PostgreSQL) + pgvector**: Cơ sở dữ liệu quan hệ tích hợp vector search cho RAG.
+ **Amazon DynamoDB**: Lưu trữ Session và Context hội thoại tốc độ cao.
+ **Amazon SQS**: Đảm bảo độ tin cậy và decoupling cho hệ thống xử lý tin nhắn.
+ **AWS CDK (Cloud Development Kit)**: Triển khai toàn bộ hạ tầng dưới dạng mã (IaC) bằng Python.
