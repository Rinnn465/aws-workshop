2---
title: "Worklog Tuần 10"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.10. </b> "
---



### Mục tiêu tuần 10:

* Triển khai giao diện admin dashboard cho dự án chatbot.
* Triển khai static website trên AWS S3 và CloudFront.
* Tích hợp Route 53 và CloudFront để phục vụ website.
* Tìm hiểu và chuẩn bị tích hợp Amazon Cognito cho chức năng đăng nhập admin.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Triển khai bước đầu tiên của flow admin, thiết kế giao diện dashboard demo | 10/11/2025   | 10/11/2025      |
| 3   | - Đẩy các file code frontend lên Amazon S3, thử nghiệm static hosting của S3 <br> - Triển khai thành công static web bằng S3 | 11/11/2025   | 11/11/2025      | [Amazon S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) |
| 4   | - Tìm hiểu về CloudFront để tích hợp vào static web đã triển khai trước đó <br> - Cấu hình CloudFront distribution để tích hợp với S3 static web | 12/11/2025   | 12/11/2025      | [Amazon CloudFront Documentation](https://docs.aws.amazon.com/cloudfront/) |
| 5   | - Triển khai thành công static web trên S3 qua CloudFront và Route 53 | 13/11/2025   | 13/11/2025      | [CloudFront with S3](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GettingStarted.SimpleDistribution.html) |
| 6   | - Họp bàn luận và chỉnh sửa architecture của dự án <br> - Loại Route 53 khỏi architecture, sử dụng trực tiếp bằng domain CloudFront <br> - Tìm hiểu thêm để tích hợp chức năng login cho admin sử dụng Cognito | 14/11/2025   | 14/11/2025      | [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/) |


### Kết quả đạt được tuần 10:

* Hoàn thành thiết kế giao diện dashboard demo cho admin flow.

* Triển khai thành công static website hosting trên Amazon S3:
  * Upload frontend code lên S3 bucket
  * Cấu hình S3 bucket cho static website hosting
  * Test và verify website hoạt động đúng

* Tích hợp CloudFront với S3 static website:
  * Tạo và cấu hình CloudFront distribution
  * Kết nối CloudFront với S3 bucket
  * Tối ưu hóa performance và caching

* Triển khai hoàn chỉnh static web qua CloudFront và Route 53:
  * Cấu hình DNS với Route 53
  * Kết nối domain với CloudFront distribution
  * Kiểm tra và verify toàn bộ flow

* Điều chỉnh architecture dự án:
  * Quyết định loại bỏ Route 53 khỏi architecture
  * Sử dụng trực tiếp CloudFront domain để đơn giản hóa
  * Cập nhật và tối ưu hóa architecture diagram

* Nghiên cứu và chuẩn bị tích hợp Amazon Cognito:
  * Tìm hiểu về Cognito User Pool
  * Nghiên cứu authentication flow cho admin dashboard
  * Lên kế hoạch triển khai login functionality


