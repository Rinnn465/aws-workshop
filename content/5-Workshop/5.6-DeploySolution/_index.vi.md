---
title : "Triển khai Giải pháp"
date :  "2025-09-09" 
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

## Triển khai Giải pháp

Trong phần này, chúng ta sẽ clone repository MeetAssist và triển khai toàn bộ hạ tầng bằng AWS CDK.

### Bước 1: Clone Repository

Clone repository từ GitHub:

```bash
git clone https://github.com/AWS-Vinhomes-Chatbot/MeetAssist
cd MeetAssist
```

### Bước 2: Build Dashboard

Trước khi triển khai ứng dụng CDK, chúng ta cần build frontend dashboard.

#### Di chuyển đến thư mục frontend

```bash
cd frontend
```

#### Cài đặt dependencies

Chạy lệnh sau để cài đặt tất cả các thư viện cần thiết:

```bash
npm i
```

#### Build Dashboard

Sau khi cài đặt hoàn tất, chạy lệnh build:

```bash
npm run build
```

Sau khi quá trình hoàn tất, một thư mục `dist` sẽ được tạo, chứa file `index.html` và thư mục `assets`.

#### Quay lại thư mục gốc của project

Sử dụng lệnh này để quay lại thư mục gốc của project:

```bash
cd ..
```

### Bước 3: Triển khai CDK Application

Triển khai ứng dụng CDK. Quá trình sẽ mất khoảng **20-30 phút** để triển khai tất cả các tài nguyên.

```bash
cdk bootstrap aws://{{account_id}}/ap-northeast-1 
cdk deploy --all 
```

{{% notice note %}}
Nếu bạn gặp lỗi ở bước này, hãy đảm bảo **Docker đang chạy** trên máy tính của bạn.
{{% /notice %}}

{{% notice info %}}
Thay thế `{{account_id}}` bằng AWS Account ID thực tế của bạn. Bạn có thể tìm thấy nó bằng cách chạy:
```bash
aws sts get-caller-identity --query Account --output text
```
{{% /notice %}}

### Bước 4: Khởi tạo Database với Embeddings

Sau khi triển khai CDK hoàn tất, bạn phải chạy **DataIndexer Lambda function** để điền dữ liệu embeddings vào bảng với thông tin schema của database.

Sử dụng lệnh AWS CLI sau:

```bash
aws lambda invoke \
  --function-name DataIndexerStack-DataIndexerFunction \
  --invocation-type Event \
  response.json \
  --region ap-northeast-1
```

{{% notice tip %}}
DataIndexer function tạo vector embeddings của database schema của bạn, giúp chatbot có thể hiểu và truy vấn dữ liệu của bạn bằng ngôn ngữ tự nhiên.
{{% /notice %}}

### Bước 5: Xác minh Triển khai

Sau khi hoàn thành tất cả các bước trên, môi trường của bạn đã được triển khai và khởi tạo đầy đủ.

Bạn có thể xác minh triển khai bằng cách kiểm tra:

1. **CloudFormation Stacks**: Tất cả các stack nên hiển thị trạng thái `CREATE_COMPLETE`
2. **File outputs.json**: Chứa các URL và ID quan trọng cho việc triển khai của bạn
3. **S3 Buckets**: Các tài sản dashboard nên được tải lên
4. **Lambda Functions**: Tất cả các function nên được tạo và sẵn sàng

### Các Bước Tiếp Theo

Bây giờ bạn có thể tiếp tục:
- Cấu hình tích hợp Facebook Messenger (Phần 5.7)
- Thiết lập Admin Dashboard (Phần 5.8)
- Bắt đầu sử dụng chatbot MeetAssist (Phần 5.9)
