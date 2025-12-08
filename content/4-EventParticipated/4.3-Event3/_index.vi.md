---
title: "Event 3"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---


# Tổng kết từ sự kiện: "AWS Cloud Mastery Series #3: AWS Well-Architected – Security Pillar Workshop"

### Định hướng chương trình
Sự kiện này xoay quanh Security Pillar trong AWS Well-Architected Framework, mang đến cho học viên cái nhìn chi tiết qua năm mảng an ninh thiết yếu:

- Mảng 1: Identity & Access Management (IAM)
- Mảng 2: Detection & Continuous Monitoring
- Mảng 3: Infrastructure Protection
- Mảng 4: Data Protection
- Mảng 5: Incident Response

Bên cạnh đó, workshop còn giới thiệu sáng kiến AWS Cloud Clubs cùng những hoạt động kết nối cộng đồng người học cloud computing tại môi trường đại học.

### Diễn Giả

- **Lê Vũ Xuân An** - AWS Cloud Club Captain HCMUTE  
- **Trần Đức Anh** - AWS Cloud Club Captain SGU  
- **Trần Đoàn Công Lý** - AWS Cloud Club Captain PTIT  
- **Danh Hoàng Hiếu Nghị** - AWS Cloud Club Captain HUFLIT  

- **Huỳnh Hoàng Long** - AWS Community Builders  
- **Đinh Lê Hoàng Anh** - AWS Community Builders  

- **Nguyễn Tuấn Thịnh** - Cloud Engineer Trainee  
- **Nguyễn Đỗ Thành Đạt** - Cloud Engineer Trainee  

- **Văn Hoàng Kha** - Cloud Security Engineer, AWS Community Builder  

- **Thịnh Lâm** - FCJ Member  
- **Việt Nguyễn** - FCJ Member  

- **Mendel Grabski (Long)** - Ex-Head of Security & DevOps, Cloud Security Solution Architect  
- **Trịnh Trương** - Platform Engineer tại TymeX, AWS Community Builder  

### Các Điểm Nổi Bật

#### Khởi động với AWS Cloud Club
Chương trình bắt đầu với phần giới thiệu chương trình AWS Cloud Club:
- Môi trường rèn luyện năng lực cloud computing thông qua dự án thực chiến  
- Tiếp cận trực tiếp với mentor là những chuyên gia trong lĩnh vực AWS  
- Tạo mạng lưới kết nối và hợp tác giữa các bạn sinh viên  
- Được vận hành bởi các câu lạc bộ tại HCMUTE, SGU, PTIT, và HUFLIT  

Thông điệp cốt lõi: Cloud Clubs là cầu nối giúp sinh viên trưởng thành về chuyên môn, sự nghiệp và mối quan hệ nghề nghiệp.

#### Identity & Access Management (IAM)
IAM được đề cập như một trong những chủ đề quan trọng nhất. Những yếu tố được nhấn mạnh:

- Tuân thủ nguyên tắc Least Privilege  
- Loại bỏ root access keys ngay sau giai đoạn khởi tạo  
- Hạn chế sử dụng wildcard permission (*)  
- Triển khai AWS SSO cho việc quản lý quyền hạn tập trung trên nhiều tài khoản  
- Nắm vững SCPs – công cụ kiểm soát permission ở cấp độ organization  
- Ứng dụng Permission Boundaries để đặt giới hạn cho user và role  

Phiên làm việc cũng phân tích sâu hai cơ chế MFA – TOTP và FIDO2 – về mặt độ an toàn cũng như khả năng recovery.

Việc sử dụng Secrets Manager cùng chu trình rotation credential (create → set → test → finalize) được trình bày như một best practice cần thiết.

#### Detection & Continuous Monitoring
Chuyên mục này giải thích phương pháp AWS thiết lập hệ thống monitoring nhiều tầng:

- Management Events: các API calls, điều chỉnh configuration  
- Data Events: thao tác ở cấp object trên S3, execution logs của Lambda  
- Network Events: VPC Flow Logs  
- Tầm nhìn thống nhất xuyên suốt các tài khoản trong organization  

EventBridge được đề cập tích cực trong bối cảnh alerting và automation — đặc biệt là tính năng cross-account event routing nhằm xây dựng security workflow tập trung.

Ứng dụng "Detection-as-Code" được minh họa qua CloudTrail Lake và việc áp dụng IaC cho detection logic.

#### Amazon GuardDuty
GuardDuty được trình bày như một dịch vụ threat detection được quản lý hoàn toàn, thực hiện phân tích:

- CloudTrail events  
- VPC Flow Logs  
- DNS queries  

Hỗ trợ nhận diện các hoạt động như tắt logging, traffic mạng bất thường hay domain queries đáng ngờ.

Các tính năng mở rộng gồm: malware scanning trên S3, EKS audit log monitoring, RDS anomaly detection, Lambda network analysis, cùng runtime protection thông qua GuardDuty Agent.

Dịch vụ này được kết nối với các framework như AWS Foundational Security Best Practices và CIS Benchmarks.

#### Network Security Controls
Nội dung bảo vệ infrastructure được trình bày qua:

- Các dạng attack: Ingress, Egress, Insider  
- So sánh Security Groups (stateful) với NACLs (stateless)  
- Ứng dụng Route 53 Resolver trong môi trường hybrid  
- AWS Network Firewall: kiểm soát egress, network segmentation, IDS/IPS  
- Kết hợp threat intelligence từ GuardDuty để blocking tự động  

#### Data Protection & Governance
Những vấn đề cốt lõi về encryption và quản lý credentials:

- Kiến trúc KMS (CMK → Data Key)  
- Áp dụng IAM conditions để hạn chế các cryptographic operations  
- ACM cung cấp certificates miễn phí và tự động renewal  
- Credential rotation với Secrets Manager  
- Yêu cầu bắt buộc TLS cho S3 và DynamoDB  
- Thiết lập SSL/TLS trên RDS  

#### Incident Response & Prevention
**Best practices trong prevention:**

- Ưu tiên temporary credentials  
- Tránh để S3 buckets ở chế độ public  
- Bố trí các services quan trọng trong private subnet  
- Triển khai IaC để giữ tính consistency  
- Áp dụng two-layer approval cho các thay đổi có high-risk  

**Quy trình Incident Response 5 giai đoạn:**  
Preparation → Detection & Analysis → Containment → Eradication & Recovery → Lessons Learned.

### Liên hệ Thực tiễn
Kiến thức bảo mật thu được từ sự kiện có thể ứng dụng ngay vào dự án AI Chatbot mà nhóm đang phát triển. Việc cải thiện IAM cho phép quản lý quyền truy cập chặt chẽ hơn đối với backend và công cụ quản trị. Hệ thống logging, monitoring và các biện pháp bảo vệ cơ sở hạ tầng hỗ trợ team xây dựng quy trình giám sát minh bạch, giảm thiểu sai sót cấu hình. Khuôn khổ xử lý sự cố giúp nhóm ứng phó kịp thời và có hệ thống hơn. Tất cả những yếu tố này đóng góp vào việc tạo nên một nền tảng chatbot vững chắc và đáng tin cậy hơn.

### Cảm nhận về Sự kiện
- Chương trình được tổ chức chuyên nghiệp với các diễn giả am hiểu, trình bày dễ hiểu các chủ đề phức tạp.  
- Phần tương tác hỏi đáp tạo điều kiện cho học viên làm rõ thắc mắc và nâng cao nhận thức.

#### Một Số Hình Ảnh
![Event 3-1](/images/4-EventParticipated/event3-1.jpg)
![Event 3-2](/images/4-EventParticipated/event3-2.jpg)
