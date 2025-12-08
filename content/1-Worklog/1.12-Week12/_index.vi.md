---
title: "Worklog Tuần 12"
date: "2025-11-24"
weight: 12
chapter: false
pre: " <b> 1.12 </b> "
---



### Mục tiêu tuần 12:

* Triển khai hỗ trợ chuyển đổi theme (sáng/tối) cho admin dashboard.
* Tái cấu trúc cấu hình AWS và database schema.
* Cải thiện UI/UX với các components nâng cao.
* Triển khai tính năng quản lý lịch trình tư vấn viên.
* Tối ưu hóa infrastructure với custom resources.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Triển khai hỗ trợ chuyển đổi theme (chế độ sáng/tối) <br> - Refactor các trang để sử dụng theme styles <br> - Tăng cường UI components với loading indicators và responsive design <br> - Cải thiện accessibility và usability của forms và buttons | 24/11/2025   | 24/11/2025      |  |
| 3   | - Refactor cấu hình AWS: chuyển từ .env sang config.json <br> - Tải cấu hình từ /config.json (tự động tạo bởi CDK FrontendStack) <br> - Loại bỏ environment variables và fallback mechanisms <br> - Xóa deploy.sh script đã lỗi thời | 25/11/2025   | 25/11/2025      |  |
| 4   | - Chỉnh sửa database schema (xóa bảng CommunityProgram) <br> - Xóa ProgramsPage component và API calls <br> - Loại bỏ functions liên quan đến community program <br> - Cập nhật OverviewPage và Sidebar <br> - Thay thế icons bằng lucide-react <br> - Thêm recharts dependencies và enhance OverviewPage | 26/11/2025   | 26/11/2025      |  |
| 5   | - Refactor archive service: loại bỏ CSV mappings không sử dụng <br> - Triển khai custom resource để tạo config.json từ SSM parameters <br> - Upload config.json lên S3 | 27/11/2025   | 27/11/2025      |  |
| 6   | - Thêm API functions cho quản lý consultant schedules: <br>&emsp; + getConsultantSchedules <br>&emsp; + getScheduleByConsultant <br>&emsp; + createConsultantSchedule <br>&emsp; + updateConsultantSchedule <br>&emsp; + deleteConsultantSchedule <br>&emsp; + generateConsultantSchedule <br> - Cập nhật Admin service để xử lý schedule actions <br> - Tăng cường appointment retrieval với filters <br> - Thêm ConsultantSchedule type và error handling   | 28/11/2025   | 28/11/2025      |  |


### Kết quả đạt được tuần 12:

* Hoàn thành triển khai chuyển đổi giao diện:
  * Chế độ sáng/tối (light/dark mode)
  * Tái cấu trúc tất cả trang để sử dụng theme styles
  * Các trang: Tư vấn viên, Hội thoại, Tổng quan, Chương trình
  * Cải thiện loading indicators và thiết kế responsive

* Tái cấu trúc cấu hình AWS:
  * Chuyển từ .env sang config.json
  * Tự động tạo config bởi CDK FrontendStack
  * Loại bỏ biến môi trường (environment variables)
  * Xóa deploy.sh script cũ
  * Tải config từ /config.json endpoint

* Tối ưu hóa database schema:
  * Xóa bảng CommunityProgram không sử dụng
  * Xóa ProgramsPage component
  * Dọn dẹp API calls và admin service functions
  * Cập nhật OverviewPage và Sidebar
  * Xóa CommunityProgram interface

* Cải thiện UI/UX:
  * Thay thế icons bằng lucide-react
  * Thêm thư viện: lucide-react và recharts
  * Nâng cấp OverviewPage với biểu đồ và thẻ thống kê
  * Thiết kế hiện đại và nhất quán
  * Cải thiện khả năng tiếp cận và tính dễ sử dụng
  * Hộp thoại xác nhận tốt hơn với globalThis.confirm

* Tối ưu hóa infrastructure:
  * Tái cấu trúc archive service
  * Xóa các CSV mappings không sử dụng
  * Triển khai custom resource cho config.json
  * Tự động tạo config từ SSM parameters
  * Upload config lên S3

* Quản lý lịch trình tư vấn viên:
  * Triển khai đầy đủ các thao tác CRUD cho lịch trình tư vấn viên
  * Tự động tạo lịch trình
  * Lọc lịch hẹn theo tư vấn viên và khách hàng
  * ConsultantSchedule type đảm bảo type safety
  * Tăng cường xử lý lỗi và ghi log
  * Tích hợp với Admin service

* Cải thiện chất lượng code:
  * Type safety tốt hơn với TypeScript
  * Xử lý lỗi được cải thiện
  * Cơ chế logging nâng cao
  * Dọn dẹp và tổ chức code
  * Mẫu code nhất quán


