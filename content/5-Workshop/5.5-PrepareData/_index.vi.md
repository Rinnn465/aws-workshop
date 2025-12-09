---
title : "Chuẩn bị Dữ liệu"
date :  "2025-09-09" 
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Tải Xuống Tập Dữ Liệu và Tải Lên Amazon S3

### Bước 1: Tải Xuống Tập Dữ Liệu

1. Truy cập [MeetAssistData](https://drive.google.com/drive/folders/1JQ9X9BbKL7q82sEifvN5Seas7Mrgh4Q7?usp=sharing)
2. Tải dữ liệu về máy tính của bạn
3. Giải nén file, sẽ tạo ra một thư mục có tên `DATA`

{{% notice warning %}}
**QUAN TRỌNG - KHÔNG mở các file CSV bằng Excel:**
- **Microsoft Excel có thể tự động chuyển đổi định dạng dữ liệu**, có thể làm hỏng dữ liệu (ví dụ: số điện thoại, ngày tháng, ID có thể bị thay đổi)
- **Phương pháp khuyến nghị:** Tải dữ liệu lên S3 trước (các bước bên dưới), sau đó sử dụng **VS Code để xem/kiểm tra** các file CSV thay vì Excel
- **Nếu bạn phải xem trên local:** Chỉ sử dụng **VS Code** - nó sẽ không sửa đổi dữ liệu của bạn như Excel
- **Giữ nguyên các file CSV gốc** trước khi tải lên S3
{{% /notice %}}

### Bước 2: Tạo S3 Bucket

Chạy lệnh CLI này để tạo bucket Amazon S3. Thay thế `<account-id>` bằng AWS Account ID của bạn:

```bash
aws s3 mb s3://meetassist-data-<account-id>-ap-northeast-1 --region ap-northeast-1
```

{{% notice tip %}}
Để tìm AWS Account ID của bạn, chạy: `aws sts get-caller-identity --query Account --output text`
{{% /notice %}}

![S3 Bucket Creation](/images/5-Workshop/5.5-PrepareData/1.jpg)

### Bước 3: Tải Dữ Liệu Lên S3

1. Truy cập AWS S3 Console
2. Điều hướng đến bucket bạn vừa tạo: `meetassist-data-<account-id>-ap-northeast-1`
3. Tạo một thư mục có tên **`data`**
4. Tải tất cả các file CSV từ thư mục `DATA` đã giải nén vào thư mục `data` trong S3

![data folder](/images/5-Workshop/5.5-PrepareData/2.jpg)
![upload files](/images/5-Workshop/5.5-PrepareData/3.jpg)

### Xác Minh

Sau khi tải lên, xác minh rằng tất cả các file CSV đều có trong S3 bucket của bạn dưới prefix `data/`:

```bash
aws s3 ls s3://meetassist-data-<account-id>-ap-northeast-1/data/
```

Bạn sẽ thấy tất cả các file CSV được liệt kê trong kết quả.
