---
title: "Worklog Tuần 13"
date: "2025-12-01"
weight: 13
chapter: false
pre: " <b> 1.13 </b> "
---



### Mục tiêu tuần 13:

* Triển khai Consultant Portal với chức năng xác thực và quản lý lịch trình/lịch hẹn.
* Tích hợp Cognito User Pool cho tư vấn viên.
* Dọn dẹp code và tái cấu trúc project structure.
* Triển khai quản lý khách hàng và hệ thống thông báo email.
* Cải thiện trải nghiệm người dùng với đa ngôn ngữ.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tạo giao diện Consultant Portal <br> - Tích hợp với Consultant User Pool của Cognito <br> - Sửa các lỗi liên quan đến xác thực và API | 01/12/2025   | 01/12/2025      |  |
| 3   | - Thêm trang Login với Cognito OAuth2 <br> - Tạo Schedule page với calendar navigation <br> - Tạo Appointments page với confirm/deny functionality <br> - Implement responsive UI với Tailwind CSS <br> - Thêm backend functions: get_my_schedule, get_my_appointments, confirm/deny_appointment <br> - Sửa lỗi CORS, API paths, và account status display | 02/12/2025   | 02/12/2025      |  |
| 4   | - Dọn dẹp code: loại bỏ SSM parameters không sử dụng <br> - Xóa các API functions không cần thiết <br> - Xóa watch-sync scripts <br> - Tái cấu trúc: đổi tên admin-dashboard → frontend <br> - Chia cấu trúc file theo vai trò (admin, consultant) | 03/12/2025   | 03/12/2025      |  |
| 5   | - Dịch giao diện sang tiếng Việt cho nhiều trang <br> - Triển khai hộp thoại xác nhận cho các hành động lịch hẹn <br> - Tăng cường xử lý lỗi trong API service <br> - Tùy chỉnh mẫu email cho Consultant User Pool | 04/12/2025   | 04/12/2025      |  |
| 6   | - Triển khai quản lý khách hàng với các thao tác CRUD <br> - Xóa trường không cần thiết khỏi biểu mẫu quản lý khách hàng <br> - Thêm Lambda Email Notification (ngoài VPC) <br> - Tích hợp SES để gửi email xác nhận/hủy bỏ <br> - Mở rộng API service với các phương thức thông báo email | 05/12/2025   | 05/12/2025      |  |


### Kết quả đạt được tuần 13:

* Triển khai thành công Consultant Portal:
  * Giao diện người dùng mới cho tư vấn viên
  * Tích hợp xác thực Cognito với Consultant User Pool
  * Trang đăng nhập với OAuth2 flow
  * Giao diện responsive với Tailwind CSS

* Các trang chức năng cho Consultant Portal:
  * Schedule page: xem lịch trình hàng tuần với calendar navigation
  * Appointments page: xem, xác nhận và từ chối lịch hẹn
  * Quản lý lịch làm việc cá nhân

* API Backend cho Consultant Portal:
  * `get_my_schedule`: tư vấn viên xem lịch trình của mình
  * `get_my_appointments`: xem các lịch hẹn
  * `confirm_appointment` và `deny_appointment`: xử lý lịch hẹn
  * `get_consultant_by_email`: mapping Cognito user sang consultant_id

* Sửa lỗi và cải thiện:
  * Sửa lỗi CORS (loại bỏ allow_credentials)
  * Chuyển sang sử dụng idToken thay vì accessToken
  * Sửa lỗi đường dẫn API và truy vấn SQL
  * Cải thiện hiển thị trạng thái tài khoản (Active/Pending)
  * Tăng cường xử lý lỗi

* Dọn dẹp code và tái cấu trúc:
  * Loại bỏ SSM parameters không sử dụng
  * Xóa các API functions không dùng: getTables, getTableSchema, getDatabaseStats
  * Xóa watch-sync scripts
  * Dọn dẹp comments dư thừa (TODO, BugNote)
  * Đổi tên admin-dashboard → frontend
  * Chia cấu trúc file theo vai trò (admin/consultant)

* Đa ngôn ngữ:
  * Dịch giao diện sang tiếng Việt
  * Các trang: Tư vấn viên, Tổng quan, Lịch hẹn, Lịch làm việc
  * App services và thông báo lỗi

* Quản lý khách hàng:
  * Đầy đủ các thao tác CRUD cho quản lý khách hàng
  * Tích hợp giao diện với admin dashboard
  * Đơn giản hóa biểu mẫu (xóa trường không cần thiết)

* Hệ thống thông báo email:
  * Lambda Email Notification function (ngoài VPC)
  * Tích hợp Amazon SES
  * Tự động gửi email cho xác nhận/hủy lịch hẹn
  * Backend trả về thông tin email cho frontend
  * Frontend kích hoạt thông báo email

* Tùy chỉnh mẫu email:
  * Mẫu email Consultant User Pool
  * Thông báo tạo tài khoản bởi quản trị viên
  * Email xác minh tài khoản
  * Email xác nhận/hủy lịch hẹn

* Cải thiện trải nghiệm người dùng:
  * Hộp thoại xác nhận cho các hành động quan trọng
  * Xử lý lỗi và phản hồi người dùng tốt hơn
  * Giao diện tiếng Việt/tiếng Anh nhất quán
  * Quy trình làm việc được tối ưu hóa



