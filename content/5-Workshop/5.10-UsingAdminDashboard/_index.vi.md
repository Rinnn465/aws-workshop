---
title : "Sử dụng Admin Dashboard"
date :  "2025-09-09" 
weight : 10
chapter : false
pre : " <b> 5.10. </b> "
---

## Sử dụng Admin Dashboard

Admin Dashboard cung cấp giao diện toàn diện để quản lý tư vấn viên, lịch trình và lịch hẹn.

### Trang Tổng quan

Sau khi đăng nhập, trang chủ dashboard hiển thị:

**Thống kê Hệ thống:**
- Tổng số khách hàng
- Tổng số tư vấn viên
- Tổng số lịch hẹn

**Phân loại Lịch Hẹn:**
- Biểu đồ trực quan hiển thị lịch hẹn theo trạng thái:
  - Đang chờ (Pending)
  - Đã xác nhận (Confirmed)
  - Đã hoàn thành (Completed)
  - Đã hủy (Cancelled)

**Lịch Hẹn Gần đây:**
- Danh sách các lịch hẹn gần nhất
- Xem nhanh khách hàng, tư vấn viên, ngày và trạng thái

![Admin Dashboard Home](/images/5-Workshop/5.10-UsingAdminDashboard/1.jpg)

### Quản lý Tư vấn viên

Điều hướng đến phần **Consultants** để quản lý đội ngũ tư vấn viên.

#### Xem Tư vấn viên

- Xem tất cả tư vấn viên trong dạng bảng
- Các cột: Tên, Email, Chuyên môn, Trạng thái
- Khả năng tìm kiếm và lọc

![Consultants List](/images/5-Workshop/5.10-UsingAdminDashboard/2.jpg)

#### Thêm Tư vấn viên Mới

1. Nhấp vào nút **Add Consultant**
2. Điền thông tin tư vấn viên:
   - Họ và Tên
   - Email
   - Số điện thoại
   - Chuyên môn
   - Trình độ
3. Nhấp **Create**

{{% notice info %}}
Tạo tư vấn viên sẽ tự động tạo tài khoản Cognito tương ứng với thông tin đăng nhập tạm thời được gửi đến email của họ.
{{% /notice %}}

![Add Consultant](/images/5-Workshop/5.10-UsingAdminDashboard/3.jpg)

#### Chỉnh sửa Thông tin Tư vấn viên

1. Nhấp vào nút **Edit** bên cạnh tư vấn viên
2. Cập nhật các trường mong muốn
3. Nhấp **Save Changes**

![Edit Consultant](/images/5-Workshop/5.10-UsingAdminDashboard/4.jpg)

#### Xóa Tư vấn viên

1. Nhấp vào nút **Delete** bên cạnh tư vấn viên
2. Xác nhận xóa
3. Tài khoản Cognito của tư vấn viên cũng sẽ bị xóa


#### Reset Mật khẩu Tư vấn viên

1. Nhấp vào nút **Reset Password**
2. Mật khẩu tạm thời mới sẽ được tạo
3. Tư vấn viên sẽ nhận mật khẩu qua email



### Quản lý Lịch Hẹn

Điều hướng đến phần **Appointments** để giám sát lịch hẹn toàn diện.

#### Xem Lịch Hẹn

- Chế độ xem bảng của tất cả lịch hẹn
- Lọc theo:
  - Trạng thái (Pending, Confirmed, Completed, Cancelled)
  - Khoảng thời gian
  - Tư vấn viên
  - Khách hàng

![Schedules Management](/images/5-Workshop/5.10-UsingAdminDashboard/5.jpg)


#### Tạo Lịch Hẹn Thủ công

1. Nhấp **Create Appointment**
2. Chọn khách hàng (hoặc tạo mới)
3. Chọn tư vấn viên
4. Chọn ngày và giờ
5. Thêm ghi chú (tùy chọn)
6. Nhấp **Book Appointment**


![Create Appointment](/images/5-Workshop/5.10-UsingAdminDashboard/6.jpg)

#### Cập nhật Lịch Hẹn

1. Nhấp **Edit** trên lịch hẹn
2. Sửa đổi chi tiết (thời gian, tư vấn viên, ghi chú)
3. Nhấp **Update**

![Edit Appointment](/images/5-Workshop/5.10-UsingAdminDashboard/7.jpg)

#### Hủy Lịch Hẹn

1. Nhấp **Cancel** trên lịch hẹn
2. Tùy chọn thêm lý do hủy
3. Xác nhận hủy
4. Email thông báo sẽ được gửi

#### Thay đổi Trạng thái Lịch Hẹn

Cập nhật thủ công trạng thái lịch hẹn:
- **Pending** → **Confirmed**: Phê duyệt đặt lịch
- **Confirmed** → **Completed**: Đánh dấu đã hoàn thành
- **Bất kỳ** → **Cancelled**: Hủy lịch hẹn


Bây giờ bạn có toàn quyền kiểm soát hệ thống MeetAssist thông qua Admin Dashboard!
