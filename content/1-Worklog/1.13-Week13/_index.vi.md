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
| 5   | - Dịch UI text sang tiếng Việt cho nhiều trang <br> - Implement modal confirmation cho appointment actions <br> - Tăng cường error handling trong API service <br> - Tùy chỉnh email templates cho Consultant User Pool | 04/12/2025   | 04/12/2025      |  |
| 6   | - Triển khai customer management với CRUD operations <br> - Xóa trường không cần thiết khỏi customer management form <br> - Thêm Lambda Email Notification (ngoài VPC) <br> - Tích hợp SES để gửi email confirmation/cancellation <br> - Mở rộng API service với email notification methods | 05/12/2025   | 05/12/2025      |  |


### Kết quả đạt được tuần 13:

* Triển khai thành công Consultant Portal:
  * Giao diện người dùng mới cho tư vấn viên
  * Tích hợp Cognito authentication với Consultant User Pool
  * Login page với OAuth2 flow
  * Responsive UI với Tailwind CSS

* Các trang chức năng cho Consultant Portal:
  * Schedule page: xem lịch trình hàng tuần với calendar navigation
  * Appointments page: xem, xác nhận và từ chối lịch hẹn
  * Quản lý lịch làm việc cá nhân

* Backend APIs cho Consultant Portal:
  * `get_my_schedule`: tư vấn viên xem lịch trình của mình
  * `get_my_appointments`: xem các lịch hẹn
  * `confirm_appointment` và `deny_appointment`: xử lý lịch hẹn
  * `get_consultant_by_email`: mapping Cognito user sang consultant_id

* Sửa lỗi và cải thiện:
  * Sửa lỗi CORS (loại bỏ allow_credentials)
  * Chuyển sang sử dụng idToken thay vì accessToken
  * Sửa lỗi API paths và SQL queries
  * Cải thiện hiển thị account status (Active/Pending)
  * Enhanced error handling

* Code cleanup và refactoring:
  * Loại bỏ SSM parameters không sử dụng
  * Xóa unused API functions: getTables, getTableSchema, getDatabaseStats
  * Xóa watch-sync scripts
  * Dọn dẹp comments dư thừa (TODO, BugNote)
  * Đổi tên admin-dashboard → frontend
  * Chia cấu trúc file theo vai trò (admin/consultant)

* Đa ngôn ngữ (Localization):
  * Dịch UI text sang tiếng Việt
  * ConsultantsPage, OverviewPage, AppointmentsPage, SchedulePage
  * App services và error messages

* Customer management:
  * Full CRUD operations cho quản lý khách hàng
  * UI integration với admin dashboard
  * Simplified forms (xóa trường không cần thiết)

* Email notification system:
  * Lambda Email Notification function (ngoài VPC)
  * Tích hợp Amazon SES
  * Auto-send emails cho appointment confirmation/cancellation
  * Backend trả về email details cho frontend
  * Frontend trigger email notifications

* Email templates customization:
  * Consultant User Pool email templates
  * Account creation by admin messages
  * Account verification emails
  * Appointment confirmation/cancellation emails

* Improved user experience:
  * Modal confirmations cho critical actions
  * Better error handling và user feedback
  * Consistent Vietnamese/English UI
  * Streamlined workflows



