---
title: "Bản đề xuất"
date: "2025-09-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Chatbot Đặt lịch Thông minh trên AWS

**Ngày:** 03 tháng 12 năm 2025  
**Nhóm:** Vinhomies – Đại học FPT

---

## Mục Lục

1. [Bối Cảnh và Động Lực](#1-bối-cảnh-và-động-lực)
2. [Kiến Trúc Giải Pháp](#2-kiến-trúc-giải-pháp)
3. [Các Hoạt Động Và Sản Phẩm Bàn Giao](#3-các-hoạt-động-và-sản-phẩm-bàn-giao)
4. [Ước Tính Chi Phí Dự Kiến](#4-bảng-phân-tích-chi-phí-dự-kiến)
5. [Nhóm](#5-nhóm)
6. [Tài Nguyên & Ước Tính Chi Phí](#6-tài-nguyên--ước-tính-chi-phí)
7. [Nghiệm Thu](#7-nghiệm-thu)

## 1. BỐI CẢNH VÀ ĐỘNG LỰC

### 1.1 Tóm tắt Dự án
Chatbot Đặt lịch Thông minh trên AWS là một giải pháp hoàn toàn không máy chủ (serverless), được thiết kế để tự động hóa việc đặt lịch hẹn và hỗ trợ khách hàng thông qua Facebook Messenger.

Hệ thống tích hợp các Mô hình Ngôn ngữ Lớn (LLMs) trên Amazon Bedrock (Claude 3.5 Sonnet, Claude 3 Haiku, Claude 3 Sonnet) sử dụng cơ chế Text-to-SQL để truy vấn/thực thi SQL trên cơ sở dữ liệu PostgreSQL cho các hoạt động đặt lịch phức tạp và tạo ra các phản hồi chính xác, nhận thức ngữ cảnh.

**Các Thành phần Cốt lõi:**
* **Lớp Frontend:** Tích hợp Facebook Messenger thông qua bộ thu Webhook.
* **Lớp Xử lý:** Các hàm Lambda cho ChatHandler (Xử lý Chat), Text2SQL Handler (Xử lý Text-to-SQL), Data Indexer (Đánh chỉ mục dữ liệu).
* **Lớp Dữ liệu:** PostgreSQL (RDS) cho dữ liệu cuộc hẹn; DynamoDB cho bộ nhớ cache/phiên làm việc.
* **Lớp AI:** Amazon Bedrock với Claude 3.5 Sonnet (Text2SQL) & Claude 3 Haiku/Sonnet (ChatHandler).
* **Bảng điều khiển Admin / Cổng thông tin Tư vấn viên:** Ứng dụng React được lưu trữ trên S3 + CloudFront với xác thực Cognito.

Toàn bộ hệ thống được triển khai trên kiến trúc AWS Serverless tại khu vực Châu Á Thái Bình Dương (Tokyo), đảm bảo khả năng mở rộng, tiết kiệm chi phí và độ tin cậy vận hành.

### 1.2 Tiêu chí Thành công của Dự án

**Hiệu quả Đặt lịch Tự động:**
- Giảm khối lượng công việc đặt lịch thủ công từ **80–90%** thông qua việc tạo, sửa đổi và xử lý truy vấn cuộc hẹn do chatbot điều khiển.
- Thành công được đo lường bằng tỷ lệ phần trăm các tương tác hoàn thành mà không cần sự can thiệp của con người.

**Hiệu suất Phản hồi Hệ thống:**
- Duy trì thời gian phản hồi chatbot đầu cuối **≤ 5 giây** cho 95% tin nhắn của người dùng.
- Đo lường thông qua các số liệu CloudWatch và nhật ký ứng dụng.

**Tính Sẵn sàng của Nền tảng:**
- Đạt **99.9% thời gian hoạt động (uptime)** bằng cách sử dụng các thành phần không máy chủ AWS (Lambda, API Gateway, DynamoDB, RDS).
- Được xác minh thông qua bảng điều khiển tính sẵn sàng CloudWatch và giám sát API Gateway.
  
**Bảo mật Dữ liệu & Tuân thủ:**
- Thực thi xử lý dữ liệu an toàn bằng cách sử dụng IAM least privilege (đặc quyền tối thiểu), xác thực Cognito, Secrets Manager, cách ly VPC, SSM và VPC Endpoints.
- Tuân thủ được xác thực thông qua IAM Access Analyzer, nhật ký luồng VPC (VPC flow logs) và kiểm tra thông tin xác thực.
  
**Sự Sẵn sàng của Bảng điều khiển Vận hành:**
- Bàn giao Bảng điều khiển Admin đầy đủ chức năng cho phép các tư vấn viên theo dõi lịch trình, xem báo cáo và quản lý phiên người dùng.
- Thành công được đo lường bằng kiểm thử khả năng sử dụng và hoàn thành tất cả các quy trình làm việc của admin.
  
**Sự Ổn định của Kênh Nhắn tin:**
- Cung cấp tích hợp ổn định và không lỗi với Nền tảng Facebook Messenger (tỷ lệ lỗi webhook <1%).
- Đo lường qua tỷ lệ lỗi webhook (<1%) và các chỉ số thành công xử lý sự kiện.
  
**Xác minh Email An toàn:**
- Đảm bảo việc xác minh email OTP được gửi đi đáng tin cậy thông qua Amazon SES với tỷ lệ gửi thành công >98%.
- Đo lường bằng báo cáo gửi và chỉ số trả lại/khiếu nại của SES.
  
### 1.3 Giả định
**Điều kiện tiên quyết & Quyền truy cập:**
* Tài khoản AWS & Khu vực (Region): Giả định có sẵn một tài khoản AWS đang hoạt động. Khu vực mục tiêu là **Châu Á Thái Bình Dương (Tokyo) - ap-northeast-1** do tính khả dụng của mô hình Bedrock.
* Tài khoản Meta (Facebook): Giả định khách hàng có tài khoản Nhà phát triển Meta hợp lệ. Thông tin xác thực (App ID, Page Token) được lưu trữ trong AWS SSM/Secrets Manager.
* Xác minh Email: Email người gửi cho Amazon SES đã được xác minh.

**Sự phụ thuộc bên ngoài:**
*  Nền tảng Facebook Messenger: Frontend của chatbot phụ thuộc hoàn toàn vào sự ổn định và tính khả dụng của Facebook Messenger Graph API (v18.0). Bất kỳ thay đổi đáng kể nào đối với cấu trúc payload Webhook Facebook hoặc việc ngừng sử dụng API có thể yêu cầu cập nhật mã.
*  Tính khả dụng của LLM: Hệ thống phụ thuộc vào tính khả dụng liên tục và hạn ngạch đầy đủ của Anthropic Claude 3 Haiku (cho logic chat) và Claude 3.5 Sonnet (cho Text-to-SQL) trong Amazon Bedrock.

**Ràng buộc Kỹ thuật**
* Hỗ trợ Ngôn ngữ: Các prompt của hệ thống và tìm kiếm văn bản cơ sở dữ liệu (phần mở rộng unaccent) được tối ưu hóa cụ thể cho tiếng Việt. Giả định rằng cơ sở người dùng chính giao tiếp bằng tiếng Việt.
* Cấu trúc Dữ liệu: Dự án giả định các định dạng tệp CSV cụ thể (tên cột, kiểu dữ liệu) cho việc nhập dữ liệu ban đầu vào RDS. Bất kỳ sai lệch nào trong lược đồ dữ liệu đầu vào có thể khiến quá trình khởi tạo hoặc đánh chỉ mục thất bại.
* Giới hạn Serverless: Logic ứng dụng bị giới hạn bởi các giới hạn thực thi của AWS Lambda (ví dụ: các hàm Text2SQL và ChatHandler có thời gian chờ là 120 giây). Các truy vấn phức tạp hoặc độ trễ LLM vượt quá khoảng thời gian này có thể dẫn đến hết thời gian chờ (timeout).

**Rủi ro:** 
* Độ chính xác LLM (Ảo giác): Mặc dù kỹ thuật prompt (prompt engineering) được sử dụng để giảm thiểu lỗi, nhưng giả định rằng có rủi ro không bằng không về việc mô hình AI tạo ra các truy vấn SQL hoặc phản hồi ngôn ngữ tự nhiên không chính xác.
* Biến động Chi phí: Dự án sử dụng các dịch vụ "pay-as-you-go" (token Bedrock, lệnh gọi Lambda). Giả định khách hàng hiểu rằng chi phí vận hành sẽ biến động dựa trên lưu lượng truy cập và độ phức tạp của các tương tác người dùng.
* Quyền riêng tư Dữ liệu: Vì cơ sở dữ liệu được triển khai trong subnet riêng tư (private subnet), nó được bảo mật khỏi truy cập công cộng. Tuy nhiên, giả định rằng việc xử lý PII nhạy cảm (Thông tin nhận dạng cá nhân) tuân thủ các chính sách quản trị dữ liệu nội bộ của khách hàng, vì chatbot xử lý tên, số điện thoại và email.


## 2. KIẾN TRÚC GIẢI PHÁP

### 2.1 Sơ đồ Kiến trúc Kỹ thuật

#### 2.1.1 Mô tả Kiến trúc
Giải pháp đề xuất sử dụng kiến trúc **Serverless-First** (Ưu tiên không máy chủ) và **Event-Driven** (Hướng sự kiện) được lưu trữ trên AWS Cloud (Khu vực: ap-northeast-1), được thiết kế để đảm bảo khả năng mở rộng, bảo mật và hiệu quả chi phí tuân thủ theo AWS Well-Architected Framework.

Kiến trúc được chia thành ba lớp logic chính:

1. **Lớp Frontend & Trình bày:** 
   * Bảng điều khiển Admin & Cổng thông tin Tư vấn viên: Được lưu trữ dưới dạng Ứng dụng Một trang (SPA) trên Amazon S3 và phân phối toàn cầu qua Amazon CloudFront (CDN) để có độ trễ thấp.
   * Giao diện Chat: Tích hợp trực tiếp với Nền tảng Facebook Messenger qua Webhooks.

2. **Lớp Xử lý & Logic Kinh doanh (Được bảo mật bởi VPC):**
    * **API Gateway:** Đóng vai trò là điểm vào an toàn cho cả Webhook Facebook và các cuộc gọi API Dashboard.
    * **Xử lý Bất đồng bộ:** Để đảm bảo tính sẵn sàng cao và sự phân tách, các tin nhắn đến được đẩy vào Amazon SQS (FIFO) trước khi xử lý. Điều này ngăn mất dữ liệu trong các đợt tăng đột biến lưu lượng và đảm bảo thứ tự tin nhắn.
    * **Tính toán (Compute):** Các hàm AWS Lambda xử lý tất cả logic kinh doanh, bao gồm xác minh webhook, xử lý chat và các hoạt động CRUD của admin.
    * **Tích hợp AI:** Hệ thống tận dụng Amazon Bedrock thông qua VPC Interface Endpoints để truy cập các Mô hình Nền tảng (Claude 3 Haiku để phát hiện ý định, Claude 3 Sonnet để trích xuất và Claude 3.5 Sonnet để tạo Text-to-SQL) một cách an toàn mà không cần đi qua internet công cộng.
3. **Lớp Dữ liệu & Lưu trữ:** 
   * **Dữ liệu Quan hệ:** Amazon RDS cho PostgreSQL lưu trữ dữ liệu có cấu trúc (Tư vấn viên, Khách hàng, Cuộc hẹn). Nó được triển khai trong các subnet riêng biệt lập (private isolated subnets).
   * **Dữ liệu Phiên:** Amazon DynamoDB quản lý phiên người dùng và ngữ cảnh cuộc trò chuyện với khả năng đọc/ghi tốc độ cao.
   * **Lưu trữ:** Amazon S3 được sử dụng để lưu trữ các lần nhập dữ liệu thô và lưu trữ lịch sử thông qua các tác vụ định kỳ EventBridge.


#### 2.1.2 Cơ sở hạ tầng Mạng & Bảo mật
* **Cách ly VPC:** Tất cả tài nguyên tính toán cốt lõi (Lambda) và cơ sở dữ liệu nằm trong Đám mây Riêng Ảo (VPC) bên trong các Subnet Riêng Biệt lập, đảm bảo không tiếp xúc trực tiếp với internet công cộng.
* **VPC Endpoints:** Thay vì sử dụng NAT Gateways (tối ưu hóa chi phí), kiến trúc sử dụng VPC Gateway Endpoints (cho S3, DynamoDB) và Interface Endpoints (cho Secrets Manager, Bedrock Runtime) để giữ lưu lượng truy cập bên trong mạng AWS.
* **Xác thực:** Amazon Cognito User Pools quản lý xác thực cho các cổng thông tin Admin và Tư vấn viên. Facebook Messenger xác thực tính toàn vẹn thông qua chữ ký HMAC bằng cách sử dụng các bí mật được lưu trữ trong AWS Secrets Manager.
* **Kiểm soát Truy cập:** AWS IAM tuân theo nguyên tắc đặc quyền tối thiểu (least privilege) cho tất cả các tương tác giữa dịch vụ với dịch vụ.

#### 2.1.3 Luồng Quy trình Dữ liệu

| Bước | Luồng | Mô tả |
|---|---|---|
| 1 | Người dùng → Facebook Messenger | Người dùng gửi tin nhắn |
| 2 | FB → API Gateway → WebhookReceiver | Webhook nhận & xác thực sự kiện |
| 3 | WebhookReceiver → SQS | Tin nhắn được xếp hàng để xử lý bất đồng bộ |
| 4 | SES → Người dùng | Gửi OTP qua email |
| 5 | ChatHandler → DynamoDB | Lưu trữ bộ nhớ cache phiên & cuộc trò chuyện |
| 6 | ChatHandler → Claude 3 Haiku | Phát hiện ý định |
| 7 | Claude 3 Haiku → Claude 3 Sonnet | Phân tích ngữ cảnh, thông tin người dùng (INSERT/UPDATE lịch) |
| 8 | Text2SQL Handler → VPC Endpoint → Claude 3.5 Sonnet | Ngôn ngữ tự nhiên → SQL (SELECT + INSERT/UPDATE) |
| 9 | Text2SQL Handler → PostgreSQL | Thực thi SQL |
| 10 | SES → Tư vấn viên | Thông báo cho tư vấn viên |
| 11 | AdminManager → PostgreSQL | Quản lý dữ liệu Admin |
| 12 | EmailHandler → SES | Gửi cập nhật cuộc hẹn |
| 13 | EventBridge | Kích hoạt tác vụ hàng ngày |
| 14 | ArchiveData → S3 | Lưu trữ dữ liệu lịch sử |

#### 2.1.4 Sơ đồ Kiến trúc

![Chatbot Architecture](/images/2-Proposal/chatbot_final_final_final.drawio.png)

#### 2.1.5 Danh sách Công cụ & Dịch vụ
**Dịch vụ AWS:**
*  Tính toán: AWS Lambda
*  API: Amazon API Gateway
*  Cơ sở dữ liệu: Amazon RDS (PostgreSQL), Amazon DynamoDB
*  AI/ML: Amazon Bedrock (Claude 3 Haiku, Claude 3 Sonnet, Claude 3.5 Sonnet, Titan Embeddings)
*  Lưu trữ: Amazon S3
*  Mạng: Amazon VPC, VPC Endpoints (Gateway & Interface)
*  Phân phối Nội dung: Amazon CloudFront
*  Xác thực: Amazon Cognito
*  Nhắn tin/Hàng đợi: Amazon SQS (FIFO), Amazon SES
*  Điều phối: Amazon EventBridge
*  Quản lý: AWS CloudFormation (thông qua CDK), Systems Manager (SSM), Secrets Manager, CloudWatch

**Công cụ Phát triển:**
* IaC: AWS Cloud Development Kit (CDK) v2 (Python)
* Ngôn ngữ: Python 3.12 (Backend), TypeScript/React (Frontend)
* Container hóa: Docker (để xây dựng các lớp Lambda) 
* Kiểm soát Phiên bản: Git

### 2.2 Kế hoạch Kỹ thuật
**Cơ sở hạ tầng dưới dạng Mã (IaC) & Triển khai** 

Nhóm phát triển sẽ phát triển các tập lệnh sử dụng **AWS Cloud Development Kit (CDK) v2** với Python 3.12. Điều này sẽ cho phép triển khai nhanh chóng và lặp lại vào các tài khoản AWS bằng cách sử dụng các lệnh cdk deploy tiêu chuẩn. Toàn bộ cơ sở hạ tầng (VPC, Lambda, RDS, DynamoDB, API Gateway, Cognito) được định nghĩa trong mã, đảm bảo tính nhất quán trên các môi trường phát triển, kiểm thử và sản xuất.

**Cấu hình & Phê duyệt**

Một số cấu hình bổ sung như **Truy cập Mô hình Amazon Bedrock** (cụ thể cho Anthropic Claude 3 Haiku và Claude 3.5 Sonnet), **Xét duyệt Ứng dụng Facebook** (cho quyền pages_messaging), và **Truy cập Sản xuất Amazon SES** (để chuyển ra khỏi môi trường sandbox) có thể yêu cầu phê duyệt và sẽ tuân theo các quy trình sau:

**Chiến lược Kiểm thử**

Tất cả các đường dẫn quan trọng sẽ bao gồm phạm vi bao phủ rộng rãi, cụ thể:
* Kiểm thử Đơn vị (Unit Testing): Cho các hàm Lambda riêng lẻ (ChatHandler, Text2SQL) và các mô-đun tiện ích.
* Kiểm thử Tích hợp (Integration Testing): Xác minh luồng đầu cuối từ Facebook Messenger → API Gateway → SQS → SES →  Lambda → Bedrock → RDS.
* Kiểm thử Bảo mật (Security Testing): Xác minh các vai trò IAM least privilege và quy tắc nhóm bảo mật VPC.

### 2.3 Kế hoạch Dự án (Agile Scrum)

| Tháng | Giai đoạn | Sản phẩm bàn giao chính |
|---|---|---|
| **Tháng 9** | Học tập AWS & Thực hành Lab | Kiến thức cơ bản về AWS Serverless (Lambda, API Gateway, RDS, DynamoDB, S3), Xây dựng ứng dụng serverless cơ bản, AWS IAM & thực hành tốt nhất về bảo mật |
| **Tháng 10** | Thiết lập Cơ sở hạ tầng & AWS Nâng cao | Đi sâu vào các dịch vụ AWS nâng cao (MemoryDB, Bedrock, VPC, CDK), Triển khai cơ sở hạ tầng ban đầu (RDS, DynamoDB, Lambda layers), Mẫu AWS CDK IaC & tự động hóa |
| **Tháng 11** | Nghiên cứu, Kiến trúc & Phát triển | Thiết kế kiến trúc hệ thống (ChatHandler, Mô-đun SQL, Mô-đun RAG), Phát triển tính năng cốt lõi, Triển khai ChatHandler, Trình xử lý SQL Text-to-SQL, ScheduleExecutor & Bảng điều khiển Admin, Tích hợp Bedrock & kỹ thuật prompt LLM |
| **Tháng 12** | Kiểm thử, Tối ưu hóa & Triển khai | Kiểm thử tích hợp đầu cuối, Tối ưu hóa hiệu suất & kiểm thử tải, Chuẩn bị Demo, Triển khai cuối cùng, Tài liệu dự án & bàn giao |

### 2.4 Cân nhắc về Bảo mật
Giải pháp thực hiện cách tiếp cận "Bảo mật theo Thiết kế" (Security by Design), tận dụng các dịch vụ bảo mật gốc của AWS và các thực tiễn tốt nhất để đảm bảo tính toàn vẹn, bảo mật và sẵn sàng của dữ liệu. Các biện pháp bảo mật được phân loại thành năm miền chính:
1.  **Truy cập (Quản lý Danh tính & Truy cập)** 
      *  IAM Least Privilege: Tất cả các hàm AWS Lambda hoạt động với các vai trò IAM chi tiết chỉ cấp các quyền tối thiểu cần thiết (ví dụ: quyền truy cập bảng DynamoDB cụ thể, lệnh gọi mô hình Bedrock bị hạn chế), tuân thủ nguyên tắc đặc quyền tối thiểu.
      *  Xác thực Người dùng: Xác thực an toàn cho Bảng điều khiển Admin và Cổng thông tin Tư vấn viên được quản lý thông qua Amazon Cognito User Pools, đảm bảo quản lý danh tính tập trung và xử lý token an toàn.
      *  Xác thực Webhook: Tất cả các yêu cầu đến từ Facebook Messenger được xác thực bằng xác minh chữ ký HMAC-SHA256 (X-Hub-Signature-256) để đảm bảo tính toàn vẹn của tin nhắn và tính xác thực của nguồn gốc.
      *  Xác minh Người dùng cuối: Cơ chế OTP (Mật khẩu một lần) an toàn qua Amazon SES được triển khai để xác minh danh tính của người dùng chat trước khi xử lý các yêu cầu đặt lịch nhạy cảm.

2.  **Cơ sở hạ tầng (Bảo mật Mạng & Tính toán)** 
      * Mạng Cách ly: Tất cả tài nguyên tính toán backend (Lambda) và cơ sở dữ liệu (Amazon RDS) được triển khai trong VPC Private Isolated Subnets, không có đường vào trực tiếp từ internet công cộng.
      *  VPC Endpoints: Giao tiếp giữa các dịch vụ AWS (Lambda đến Bedrock, Secrets Manager, S3, DynamoDB) diễn ra riêng tư qua VPC Interface và Gateway Endpoints, giữ lưu lượng hoàn toàn trong mạng trục AWS.
      *  Mã hóa khi Truyền tải: Tất cả lưu lượng mạng được mã hóa bằng TLS 1.2+ thông qua Amazon API Gateway và CloudFront.

3.  **Dữ liệu (Bảo vệ & Quyền riêng tư)** 
      *  Quản lý Bí mật: Thông tin xác thực nhạy cảm (mật khẩu cơ sở dữ liệu, Facebook Page Tokens) được lưu trữ và truy xuất an toàn từ AWS Secrets Manager và SSM Parameter Store. Không có bí mật nào được mã hóa cứng trong mã nguồn ứng dụng.
      *  Ngăn chặn SQL Injection: Lớp Text-to-SQL thực hiện các rào chắn nghiêm ngặt, bao gồm:
          *  Sử dụng các truy vấn tham số hóa (thông qua psycopg) để vô hiệu hóa các cuộc tấn công tiêm nhiễm.
          *  Xác thực đầu ra LLM để khớp chính xác với các tham số lược đồ cơ sở dữ liệu.
          *  Các lớp ủy quyền để hạn chế các thay đổi cơ sở dữ liệu (INSERT/UPDATE) dựa trên ý định của người dùng.

4.  **Phát hiện (Ghi nhật ký & Giám sát)** 
      *  Ghi nhật ký Tập trung: Nhật ký ứng dụng, dấu vết lỗi và nhật ký truy cập được tổng hợp trong Amazon CloudWatch Logs để phân tích thời gian thực và khắc phục sự cố.
5.  **Quản lý Sự cố:**
      *  Khả năng phục hồi & Chuyển đổi dự phòng: Hệ thống bao gồm xử lý tích hợp cho việc điều tiết dịch vụ (ví dụ: giới hạn tốc độ Bedrock) và cơ chế thử lại theo cấp số nhân (exponential backoff) để duy trì sự ổn định trong khi xảy ra sự cố.

---

## 3. CÁC HOẠT ĐỘNG VÀ SẢN PHẨM BÀN GIAO

### 3.1 Hoạt động và sản phẩm bàn giao

| Giai đoạn Dự án | Thời gian | Hoạt động | Sản phẩm bàn giao | Nỗ lực (M/D) |
|---|---|---|---|---|
| **Học tập AWS & Thực hành** | Tháng 9 – Tháng 10 (8 tuần) | Thực hành kiến thức cơ bản AWS (Lambda, API Gateway, RDS, DynamoDB); Lập kế hoạch cơ sở hạ tầng; Thiết kế kiến trúc | Hoàn thành các bài lab AWS cốt lõi; Kiến trúc kỹ thuật; Tài liệu thiết kế cơ sở hạ tầng | 120 |
| **Nghiên cứu & Phát triển** | Đầu tháng 11 – Giữa tháng 11 (2 tuần) | Hoàn thiện kiến trúc hệ thống; Thiết kế mô-đun SQL; Xác nhận ngăn xếp công nghệ | Sơ đồ kiến trúc hệ thống chi tiết; Đặc tả mô-đun; Báo cáo lựa chọn công nghệ | 30 |
| **Phát triển Hệ thống Cốt lõi** | Giữa tháng 11 – Cuối tháng 11 (2.5 tuần) | Xây dựng WebhookReceiver; Phát triển ChatHandler; Mô-đun Text-to-SQL; Quản lý phiên; Tích hợp Amazon Bedrock | Dịch vụ WebhookReceiver; ChatHandler với logic đặt lịch; Bộ xử lý Text-to-SQL; Chatbot hoạt động đầy đủ | 12.5 |
| **Triển khai Cơ sở hạ tầng** | Giữa tháng 11 – Cuối tháng 11 (2 tuần) | Thiết lập VPC; Triển khai Lambda, RDS/DynamoDB; Cấu hình Secrets Manager; Thiết lập API Gateway | Cơ sở hạ tầng AWS đã triển khai; Các hàm Lambda; Cơ sở dữ liệu; Cấu hình nhóm bảo mật | 30 |
| **Bảng điều khiển Admin/Cổng thông tin Tư vấn viên & Tính năng** | Cuối tháng 11 – Đầu tháng 12 (2 tuần) | Dashboard Frontend (React/TypeScript); Trang phân tích; Quản lý tư vấn viên; Đặt lịch cho Admin; Đặt lịch cho tư vấn viên | Bảng điều khiển admin/cổng thông tin tư vấn viên đầy đủ chức năng; Thành phần UI; Biểu đồ và trực quan hóa dữ liệu | 25 |

### 3.2 NGOÀI PHẠM VI (OUT OF SCOPE)
**Tích hợp Kênh Giao tiếp**
*  Tích hợp đa kênh ngoài Facebook Messenger (ví dụ: WhatsApp, Line, Telegram, widget chat trên web)
*  Tích hợp cuộc gọi thoại hoặc hỗ trợ khách hàng dựa trên IVR
*  Cải tiến AI/ML
*  Mô-đun RAG (Retrieval-Augmented Generation) sử dụng các cơ sở kiến thức bên ngoài
*  Tinh chỉnh (Fine-tuning) hoặc tùy chỉnh các mô hình LLM ngoài các dịch vụ tiêu chuẩn của Amazon Bedrock

**Cơ sở hạ tầng**
*  Triển khai chuyển đổi dự phòng đa vùng và phục hồi sau thảm họa
*  Các chiến lược tối ưu hóa chi phí nâng cao hoặc quản lý dự báo năng lực

**Phân tích & Báo cáo**
*  Phân tích dự đoán cho các xu hướng tư vấn
*  Tích hợp với các nền tảng BI (Tableau, Power BI)

### 3.3 LỘ TRÌNH LÊN PRODUCTION 
Proof of Concept (POC) được kiến trúc để chứng minh giá trị cốt lõi của Chatbot Đặt lịch Thông minh sử dụng phương pháp tiếp cận ưu tiên serverless trên AWS. Mặc dù POC thiết lập luồng đặt lịch đầu cuối chức năng qua Facebook Messenger, nhưng phạm vi của nó là để xác thực tính khả thi về kỹ thuật và trải nghiệm người dùng hơn là để hỗ trợ ngay lập tức khối lượng công việc sản xuất đồng thời cao.

**Khả năng & Trọng tâm Hiện tại của POC**: Bản phát hành hiện tại tập trung vào các trường hợp sử dụng mục tiêu và xác thực kỹ thuật sau:

*  Tích hợp Cốt lõi: Tích hợp hai chiều liền mạch với Facebook Messenger qua Webhooks và Graph API.
*  Xác thực Kiến trúc: Xác thực ngăn xếp AWS Serverless (Lambda, API Gateway, DynamoDB, RDS) về hiệu quả chi phí và xử lý hướng sự kiện.
*  Logic AI: Triển khai các khả năng Text-to-SQL sử dụng Amazon Bedrock (Claude 3.5 Sonnet) để truy vấn chính xác tính khả dụng và sửa đổi dữ liệu lịch trình một cách an toàn.
*  Giao diện Quản lý: Bảng điều khiển Admin và Cổng thông tin Tư vấn viên chức năng để quản lý lịch trình thời gian thực và giám sát người dùng.
*  Hiệu suất: Tối ưu hóa ban đầu về cold start (khởi động nguội) và độ trễ phản hồi của LLM để đảm bảo trải nghiệm người dùng chấp nhận được.

**Phân tích Khoảng cách & Lộ trình Sản xuất**: Để chuyển đổi từ POC hiện tại sang một hệ thống sản xuất cấp doanh nghiệp, kiên cường hoàn toàn, giải pháp yêu cầu đầu tư thêm vào sự xuất sắc trong vận hành, hỗ trợ đa kênh và phân tích nâng cao. Lộ trình sau đây phác thảo các giai đoạn chính để giải quyết những khoảng cách này:
*  Giai đoạn 2 - Mở rộng Đa kênh: Mở rộng giao diện chatbot ra ngoài Facebook Messenger để bao gồm Web Widget (cho các trang web doanh nghiệp) và Ứng dụng Di động chuyên dụng, đảm bảo trải nghiệm khách hàng thống nhất trên các điểm tiếp xúc.
*  Giai đoạn 3 - Tối ưu hóa Chi phí & Hiệu suất AI: Chuyển đổi từ các Mô hình Nền tảng đa năng sang các Mô hình Ngôn ngữ Nhỏ (SLMs) được tinh chỉnh cụ thể cho các tác vụ tạo SQL. Các mô hình này sẽ được lưu trữ trên Amazon EC2/SageMaker để giảm độ trễ suy luận và chi phí vận hành ở quy mô lớn.
*  Giai đoạn 4 - Phân tích Dữ liệu Nâng cao: Triển khai đường ống AWS Glue + Amazon Athena để thực hiện phân tích sâu về nhật ký cuộc trò chuyện và xu hướng đặt lịch, cho phép đưa ra các quyết định kinh doanh dựa trên dữ liệu ngoài việc báo cáo vận hành đơn giản.
*  Giai đoạn 5 - Sự xuất sắc trong Vận hành & Khả năng mở rộng: Triển khai các chiến lược tự động mở rộng toàn diện trên tất cả các lớp để xử lý tải lưu lượng truy cập biến động một cách linh hoạt. Điều này bao gồm Provisioned Concurrency cho các hàm Lambda để loại bỏ cold start, tự động mở rộng lưu trữ cho RDS và EC2 Auto Scaling Groups cho đội xe suy luận LLM đã tinh chỉnh. Ngoài ra, nâng cao khả năng quan sát bằng cách triển khai theo dõi phân tán AWS X-Ray và bảng điều khiển CloudWatch tùy chỉnh để phát hiện bất thường chủ động và quản lý sự cố.
*  Giai đoạn 6 - Tính sẵn sàng cao & Phục hồi sau thảm họa: Triển khai đa vùng (Active-Passive) để đảm bảo tính liên tục kinh doanh và độ sẵn sàng 99.99% trong trường hợp gián đoạn dịch vụ khu vực.
---

## 4. BẢNG PHÂN TÍCH CHI PHÍ DỰ KIẾN

**Khu vực:** ap-northeast-1 (Tokyo) | **Nguồn:** [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=ee545a5e20d05d16fbf6eab1e4e66a35b70a2323) | Ngày ước tính: 8 tháng 12 năm 2025 

| Dịch vụ AWS | Chi phí Hàng tháng (USD) | Chi phí 12 Tháng | Mô tả / Cấu hình |
|---|---|---|---|
| **Amazon VPC** | $20.45 | $245.40 | Bảo mật Mạng: 2 VPC Interface Endpoints (PrivateLink) để bảo mật lưu lượng giữa Lambda, Bedrock, và Secrets Manager. |
| **Amazon Bedrock** | $9.08 | $108.96 | Các mô hình AI Agents: Chi phí kết hợp cho Claude 3 Haiku (Chat/Ý định), Claude 3 Sonnet (Phân tích Ngữ cảnh), và Claude 3.5 Sonnet (Text2SQL).  |
| **Amazon RDS** | $5.83 | $69.96 | Cơ sở dữ liệu: db.t3.micro, 20 GB Lưu trữ GP2, Triển khai Single-AZ, ước tính sử dụng 15%/tháng. |
| **Amazon Cognito** | $0.50 | $6.00 | 10 MAU với Bảo mật Nâng cao. |
| **Amazon SQS** | $0.50 | $6.00 | Hàng đợi FIFO, 1M yêu cầu/tháng. |
| **AWS Secrets Manager** | $0.40 | $4.80 | Bảo mật: 1 bí mật được lưu trữ, bật tự động xoay vòng (khoảng thời gian 30 ngày). |
| **Amazon DynamoDB** | $0.28 | $3.36 | On-Demand, 1 GB lưu trữ. |
| **Amazon CloudFront** | $0.12 | $1.44 | CDN: 1 GB truyền dữ liệu ra, 1,000 yêu cầu HTTPS/tháng. |
| **Amazon SES** | $0.05 | $0.60 | Dịch vụ Email: Ước tính xử lý 10 email/ngày (OTP & Thông báo). |
| **Amazon S3** | $0.03 | $0.36 | 1 GB Lưu trữ Tiêu chuẩn. |
| **API Gateway** | $0.00 | $0.00 | Được bao gồm trong AWS Free Tier (ước tính 1,000 yêu cầu/tháng). |
| **AWS Lambda** | $0.00 | $0.00 | Được bao gồm trong AWS Free Tier (ước tính 100 yêu cầu/tháng). |
| **EventBridge** | $0.00 | $0.00 | Được bao gồm trong AWS Free Tier (ước tính 10 sự kiện tùy chỉnh/tháng). |
| **TỔNG CỘNG** | **$37.24** | **$446.88** | **Trả trước: $0.00** |

**Giả định & Chiến lược Tối ưu hóa Chi phí**
1. **Thông số Mô hình Bedrock**: Công cụ tính giá AWS sử dụng các định danh chung cho các mô hình Bedrock. Đề xuất này sử dụng cụ thể Anthropic Claude 3 Haiku cho phát hiện ý định độ trễ thấp, Claude 3 Sonnet cho suy luận/ngữ cảnh và Claude 3.5 Sonnet cho tạo Text-to-SQL phức tạp. Chi phí ước tính phản ánh việc sử dụng kết hợp các mô hình này cho mục đích trình diễn.
2. **Tối ưu hóa VPC Endpoint**: Các VPC Interface Endpoints hiện chiếm ~55% chi phí ước tính hàng tháng ($20.45). Vì đây là Proof of Concept (POC), các endpoint này có thể được hủy cung cấp (de-provisioned) khi không kiểm thử tích cực để giảm đáng kể chi phí thực tế.
3. **Sử dụng Mô hình AI**: Chi phí Bedrock thay đổi dựa trên mức tiêu thụ token. Ước tính giả định lưu lượng kiểm thử vừa phải; chi phí sản xuất sẽ tăng tuyến tính với khối lượng người dùng thực tế.
4. **Sử dụng Instance**: Instance RDS (db.t3.micro) được ước tính ở mức sử dụng 15%. Đối với môi trường phát triển, cơ sở dữ liệu có thể được dừng ngoài giờ làm việc để tiết kiệm khoảng 60-70% chi phí RDS hàng giờ.
5. **Tận dụng Free Tier**: Kiến trúc tối đa hóa việc sử dụng AWS Free Tier cho tính toán (Lambda), quản lý API (API Gateway) và điều phối (EventBridge) để giữ chi phí vận hành cơ bản ở mức tối thiểu.


---

## 5. NHÓM

### Nhà tài trợ Điều hành Khách hàng & Các bên liên quan
| Tên | Chức danh | Vai trò / Trách nhiệm | Email / Thông tin liên hệ
|---|---|---| ---|
| **Nguyễn Gia Hưng** | Head of Solutions Architect (AWS FCJ Lead) | Nhà tài trợ Điều hành & Mentor: Đóng vai trò là cố vấn kỹ thuật chính, cung cấp xác thực kiến trúc cấp cao, hướng dẫn chiến lược và đảm bảo giải pháp tuân thủ các thực tiễn tốt nhất của AWS. | hunggia@amazon.com |
| **Các Mentor AWS FCJ** | Giảng viên Chương trình | Các bên liên quan của Dự án: Chịu trách nhiệm quản trị học thuật, đánh giá các sản phẩm bàn giao của dự án theo tiêu chuẩn chương trình và phê duyệt tín chỉ thực tập. | Kênh FCJ – FPTU |

### Nhóm Dự án Đối tác
| Tên | Vai trò | Trách nhiệm | Email / Thông tin liên hệ |
|---|---|---|---|
| **Phan Quốc Anh** | Trưởng nhóm Kỹ thuật / Full-stack | **Kiến trúc sư Giải pháp (Đồng Trưởng nhóm):** Đồng thiết kế kiến trúc AWS serverless. Dẫn dắt Luồng AI & Chatbot (Tích hợp Bedrock, Logic Text2SQL, ChatHandler). Chịu trách nhiệm đánh giá tính khả thi về kỹ thuật. | pqa1085@gmail.com  0379729847 |
| **Đặng Trường Hưng** | Kỹ sư Full-stack | **Nhà phát triển & QA:** Đồng thiết kế kiến trúc AWS serverless. Người đóng góp chính cho Luồng Ứng dụng & Dashboard. Chịu trách nhiệm triển khai đầu cuối Bảng điều khiển Admin (Frontend) và logic backend Lambda phức tạp. Dẫn dắt Đảm bảo Chất lượng (QA) hệ thống, kiểm thử. | fptutruonghung@gmail.com 0937726869 |
| **Hoàng Lê Thành Đức** | PM / Full-stack | **Kiến trúc sư Giải pháp (Đồng Trưởng nhóm):** Đồng thiết kế kiến trúc AWS serverless. Dẫn dắt Luồng Ứng dụng & Dashboard (Bảng điều khiển Admin, Cổng thông tin Tư vấn viên, Logic Backend). Chịu trách nhiệm điều phối dự án và theo dõi tiến độ. | fptuduchoang@gmail.com 0829497169 |

---

## 6. TÀI NGUYÊN & ƯỚC TÍNH CHI PHÍ

| Tài nguyên | Trách nhiệm | Tỷ lệ (USD) / Giờ |
|---|---|---|
| Kiến trúc sư Giải pháp <span style="background-color: yellow;">[2]</span> | Thiết kế Kiến trúc Hệ thống, Lập kế hoạch Bảo mật, Lựa chọn Công nghệ, Đánh giá Kỹ thuật | $0 |
| Kỹ sư <span style="background-color: yellow;">[3]</span> | Phát triển Full-stack, Triển khai Cơ sở hạ tầng (IaC), Kiểm thử, Đảm bảo Chất lượng | $0 |
| Khác (Vui lòng ghi rõ) | | $0 |


<span style="background-color: yellow;">* Lưu ý: Tham khảo phần "hoạt động & sản phẩm bàn giao" để biết danh sách các giai đoạn dự án</span>

| Giai đoạn Dự án | Kiến trúc sư Giải pháp (Giờ) | Kỹ sư (Giờ) | Tổng số Giờ |
|---|---|---|---|
| Học tập AWS & Thực hành Hands-On | 320 | 640 | 960 |
| Nghiên cứu & Phát triển | 140 | 100 | 240 |
| Phát triển Hệ thống Cốt lõi | 20 | 80 | 100 |
| Triển khai Cơ sở hạ tầng | 80 | 160 | 240 |
| Bảng điều khiển Admin/Cổng thông tin Tư vấn viên | 40 | 160 | 200 |
| **Tổng số Giờ** | **600** | **1,140** | **1,740** |
| **Tổng Chi phí** | $0$ | $0 | $0 |


Phân bổ đóng góp chi phí giữa Đối tác, Khách hàng, AWS:

| Bên | Đóng góp (USD) | % Đóng góp trên Tổng số |
|---|---|---|
| Khách hàng | $0 | $0 |
| Đối tác | $0 | $0 |
| AWS | $600 | 100% |

---

## 7. NGHIỆM THU

### 7.1 QUY TRÌNH ĐÁNH GIÁ (EVALUATION PROCESS)
Vì đây là dự án Proof of Concept (POC) trong khuôn khổ chương trình đào tạo, quy trình nghiệm thu sẽ tập trung vào việc chứng minh tính khả thi của giải pháp:

1.  **Triển khai & Kiểm tra nội bộ:** Nhóm dự án tự kiểm tra (Self-test) để đảm bảo các luồng chính hoạt động trên môi trường AWS.
2.  **Buổi Demo Chính thức:** Nhóm thực hiện demo trực tiếp các kịch bản sử dụng (Use-cases) đã cam kết trước Mentor/Giảng viên.
3.  **Phản hồi:** Nhận xét từ Mentor về chức năng và kiến trúc.
4.  **Hoàn thiện:** Chỉnh sửa các lỗi nghiêm trọng (nếu có) ảnh hưởng đến luồng chính và nộp báo cáo tổng kết.

### 7.2 TIÊU CHÍ NGHIỆM THU (ACCEPTANCE CRITERIA)
Dự án được coi là hoàn thành khi đáp ứng các tiêu chí chức năng cơ bản sau (chấp nhận các lỗi nhỏ về giao diện hoặc các trường hợp biên chưa xử lý hết):

**1. Hạ tầng AWS (Infrastructure):**
*   Hệ thống được triển khai thành công trên AWS (không chạy local).
*   Các dịch vụ chính (Lambda, RDS, Bedrock) kết nối được với nhau.

**2. Chức năng Chatbot (Core Flow):**
*   **Kịch bản suôn sẻ (Happy Path):** Chatbot có thể thực hiện thành công một quy trình đặt lịch từ đầu đến cuối (Hỏi -> Kiểm tra -> Đặt -> Lưu vào DB) trong điều kiện mạng bình thường.
*   **Phản hồi:** Chatbot trả lời được các câu hỏi đúng trọng tâm (dựa trên khả năng của mô hình AI hiện tại).

**3. Website Quản lý (Admin Dashboard / Cổng thông tin Tư vấn viên):**
*   Truy cập được vào trang web qua đường dẫn CloudFront/S3.
*   Đăng nhập thành công bằng tài khoản Admin và Tư vấn viên.
*   Hiển thị được dữ liệu lịch hẹn từ cơ sở dữ liệu (có thể có độ trễ nhỏ).

**4. Tài liệu:**
*   Cung cấp đầy đủ Source Code trên GitHub.
*   Tài liệu hướng dẫn cài đặt (Readme) và báo cáo kiến trúc dự án.

---
Tải xuống tài liệu đề xuất đầy đủ: [MeetAssist Chatbot Đặt lịch Thông minh](/images/2-Proposal/Proposal_Template.docx)