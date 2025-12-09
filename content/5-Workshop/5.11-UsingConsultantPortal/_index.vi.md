---
title : "Sử dụng Consultant Portal"
date :  "2025-09-09" 
weight : 11
chapter : false
pre : " <b> 5.11. </b> "
---

## Sử dụng Consultant Portal

Consultant Portal là giao diện chuyên dụng cho các tư vấn viên để quản lý lịch hẹn và xem lịch trình của họ.

### Truy cập Consultant Portal

1. Mở Consultant Portal URL từ file `outputs.json` hoặc URL từ Outputs của FrontendStack trong bảng điều khiển AWS CloudFormation.
2. Đăng nhập bằng email và mật khẩu tư vấn viên của bạn
3. Người dùng lần đầu sẽ cần thay đổi mật khẩu tạm thời

{{% notice info %}}
Tài khoản tư vấn viên được tạo bởi quản trị viên thông qua Admin Dashboard. Bạn sẽ nhận thông tin đăng nhập qua email.
{{% /notice %}}

### Trang My Appointments

Trang **My Appointments** là trung tâm quản lý tất cả các cuộc hẹn đã lên lịch của bạn.

#### Xem Lịch Hẹn

Xem tất cả lịch hẹn của bạn trong dạng bảng với:
- Tên và liên hệ khách hàng
- Ngày và giờ hẹn
- Trạng thái (Pending, Confirmed, Completed, Cancelled)

![My Appointments](/images/5-Workshop/5.11-UsingConsultantPortal/1.jpg)

#### Lọc Lịch Hẹn

Sử dụng các tùy chọn lọc để thu hẹp chế độ xem:
- **Theo Trạng thái**: Chỉ hiển thị lịch hẹn đang chờ, đã xác nhận hoặc đã hoàn thành
- **Theo Khoảng Thời gian**: Xem lịch hẹn cho các khoảng thời gian cụ thể


#### Thao tác với Lịch Hẹn

Với mỗi lịch hẹn, bạn có thể:

**Xem Chi tiết:**
- Nhấp vào lịch hẹn để xem đầy đủ thông tin khách hàng
- Xem lại ghi chú lịch hẹn
- Kiểm tra lịch sử đặt lịch

**Xác nhận Lịch Hẹn:**
- Thay đổi trạng thái từ Pending sang Confirmed
- Khách hàng nhận thông báo email tự động

**Hoàn thành Lịch Hẹn:**
- Đánh dấu lịch hẹn là Completed sau cuộc gặp


**Hủy Lịch Hẹn:**
- Hủy lịch hẹn với lý do
- Hệ thống gửi email hủy đến khách hàng

{{% notice warning %}}
Bạn không thể trực tiếp sửa đổi thời gian hoặc ngày hẹn. Liên hệ quản trị viên nếu cần thay đổi.
{{% /notice %}}



### Trang My Schedule

Trang **My Schedule** hiển thị lịch làm việc hàng tuần của bạn.

#### Chế độ xem Hàng tuần

- Xem các khung giờ của bạn được sắp xếp theo ngày trong tuần
- Trạng thái khung giờ có mã màu:
  - **Xanh lá**: Có sẵn
  - **Xám**: Đã đặt/Không khả dụng




#### Lịch trình Chỉ xem

{{% notice info %}}
Tư vấn viên có quyền truy cập **chỉ đọc** vào lịch trình của họ. Tất cả các sửa đổi lịch trình phải được thực hiện bởi quản trị viên thông qua Admin Dashboard.
{{% /notice %}}

### Xử lý Sự cố

**Vấn đề: Không thể đăng nhập**
- Xác minh bạn đang sử dụng đúng Consultant Portal URL (không phải Admin Dashboard)
- Reset mật khẩu nếu cần


Bây giờ bạn đã sẵn sàng quản lý hiệu quả các lịch hẹn tư vấn của mình thông qua Consultant Portal!
