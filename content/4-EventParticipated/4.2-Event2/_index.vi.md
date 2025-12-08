---
title: "Event 2"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Tổng kết từ sự kiện: "AWS Cloud Mastery Series #2 – DevOps on AWS"

### Trọng tâm chương trình

- Khám phá Infrastructure as Code (IaC) cùng các công cụ hỗ trợ chính.
- Hướng dẫn xây dựng CI/CD pipeline và giới thiệu các AWS DevOps services.
- Minh họa cách triển khai monitoring và observability hiệu quả với native AWS services.
- Tổng quan về container workloads và các mô hình deployment trên AWS.

### Danh Sách Diễn Giả

- **Trương Quang Tình** – AWS Community Builder, Platform Engineer (TymeX)  
- **Bảo Huỳnh** – AWS Community Builder  
- **Nguyễn Khánh Phúc Thịnh** – AWS Community Builder  
- **Trần Đại Vĩ** – AWS Community Builder  
- **Huỳnh Hoàng Long** – AWS Community Builder  
- **Phạm Hoàng Quý** – AWS Community Builder  
- **Nghiêm Lê** – AWS Community Builder  
- **Đinh Lê Hoàng Anh** – Cloud Engineer Trainee, First Cloud AI Journey

### Những điểm chính

### **1. Văn hóa và tư duy DevOps**

Diễn giả chỉ rõ rằng DevOps vượt xa chức danh công việc – đây là sự hình thành các thói quen để nâng cao hiệu quả triển khai:
- Tự động hóa các tác vụ lặp đi lặp lại  
- Chia sẻ kiến thức giữa các vai trò  
- Liên tục thử nghiệm và học hỏi  
- Theo dõi các kết quả đo lường được thay vì dựa vào giả định  

Workshop cũng nhấn mạnh những sai lầm phổ biến: phụ thuộc quá nhiều vào tutorials mà không xây dựng dự án thực tế, hoặc so sánh với người khác thay vì tập trung vào sự tiến bộ đều đặn của bản thân.

---

### **2. Phương pháp Infrastructure as Code**

Thay vì gắn bó với một công cụ duy nhất, diễn giả so sánh nhiều cách tiếp cận IaC:

- **CloudFormation** – native AWS template engine  
- **CDK** – dành cho developers muốn định nghĩa infrastructure bằng programming languages  
- **Terraform** – tối ưu cho môi trường multi-cloud provider  

Stack, Construct, State file và abstraction layers được làm rõ qua các ví dụ thực tế.

Điểm nhấn quan trọng: infrastructure được xây dựng lại với IaC mang lại *tính nhất quán và dễ bảo trì* vượt trội so với cấu hình thủ công.

---

### **3. Container workloads và mô hình Deployment**

Workshop tiến triển từ cơ bản đến nâng cao, bắt đầu với Dockerfile concepts và quy trình tạo image. Tiếp theo là đi sâu vào các AWS services:

- **ECR** cho container image storage và scanning  
- **ECS & EKS** để orchestration  
- **App Runner** phục vụ các teams muốn deploy mà không cần cluster management  

Phân tích chi tiết giữa ECS và EKS giúp xác định use case phù hợp cho từng service.

---

### **4. Monitoring và Distributed Tracing**

Phần cuối chương trình tập trung vào AWS CloudWatch và X-Ray:

- CloudWatch đóng vai trò trung tâm cho metrics, dashboards, alarms và logs  
- X-Ray hỗ trợ trực quan hóa request flows và xác định latency bottlenecks  

Diễn giả nhấn mạnh: observability cần được tích hợp từ ban đầu trong kiến trúc hệ thống, không phải là bổ sung cuối cùng.

---
### Những điều rút ra
- Monitoring & observability phải được tích hợp từ giai đoạn thiết kế kiến trúc đầu tiên, không phải bổ sung sau, để đảm bảo tính ổn định hệ thống và phát hiện sự cố nhanh chóng.
- Hiểu rõ sự khác biệt giữa các AWS container services (ECR, ECS, EKS, App Runner) giúp lựa chọn giải pháp tối ưu cho các use cases cụ thể.
- Việc lựa chọn IaC tool (CloudFormation, CDK, Terraform) cần dựa trên yêu cầu của team và ràng buộc của dự án.
- Infrastructure as Code (IaC) mang lại tính nhất quán và khả năng bảo trì vượt trội so với cấu hình thủ công.
- Tự động hóa, chia sẻ kiến thức, thử nghiệm liên tục và đo lường kết quả là các yếu tố thiết yếu cho thành công của DevOps.
- DevOps vượt xa chức danh công việc – đây là tư duy và tập hợp thói quen nhằm cải thiện việc phát hành phần mềm.


### Ứng dụng thực tế

#### Nghiên cứu tình huống: Dự án AI Chatbot trên AWS

Kiến thức từ workshop được lên kế hoạch để tích hợp vào phát triển AI Chatbot nếu có cơ hội. Cách tiếp cận triển khai như sau:

- **Phương pháp Infrastructure as Code:** Sử dụng AWS CDK để định nghĩa toàn bộ infrastructure stack (Lambda functions, API Gateway, DynamoDB tables, S3 buckets, IAM roles, etc.) dưới dạng code, cho phép tái sử dụng dễ dàng và mở rộng hệ thống nhất quán.
- **Thiết lập CI/CD pipeline:** Triển khai AWS CodePipeline để tự động hóa các quy trình build, test và deployment đến môi trường production, đảm bảo mọi cập nhật code đều được kiểm thử và triển khai tự động.

Với DevOps practices và tích hợp AWS services, dự án AI chatbot có thể đạt được phát triển nhanh, triển khai liên tục, và duy trì khả năng mở rộng dễ dàng khi cần thiết.


### Trải nghiệm Workshop
- Workshop mang đến góc nhìn thực tiễn về cách các tổ chức hiện đại tiếp cận triển khai DevOps trên AWS.
- Diễn giả kết hợp kiến thức lý thuyết với nhiều ví dụ thực tế, làm rõ các công cụ như CloudFormation, CDK, Terraform cùng với vận hành container và các phương pháp deployment trên AWS.
- Sự kiện tạo cơ hội networking tuyệt vời với những người có cùng sở thích và tiếp thu những kinh nghiệm thực tế từ các diễn giả giàu kinh nghiệm.
#### Hình ảnh sự kiện
![Event 2-1](/images/4-EventParticipated/event2-1.jpg)
![Event 2-2](/images/4-EventParticipated/event2-2.jpg)
![Event 2-3](/images/4-EventParticipated/event2-3.jpg)


