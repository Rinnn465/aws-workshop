---
title: "Worklog Tuần 7"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---


### Mục tiêu tuần 7:

* Học cách **vẽ và thiết kế kiến trúc AWS** sử dụng draw.io theo best practices.
* Tiếp tục phát triển và **hoàn thiện pre-architecture** cho dự án chatbot.
* Xác định **hướng đi** cho dự án, bao gồm các tính năng và use cases chính.
* Nghiên cứu cơ chế **Text-to-SQL** và cách áp dụng LLM để chuyển đổi ngôn ngữ tự nhiên thành SQL queries.
* Phân tích các vấn đề về **bảo mật database** khi chatbot tương tác trực tiếp với DB (giới hạn quyền, kiểm soát truy cập).
* **Ôn tập kiến thức nền tảng AWS** để chuẩn bị cho bài kiểm tra.

---

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ---------- | ------------- | ---------------- | --------------- |
| 2 | - Học cách **vẽ kiến trúc AWS** qua video hướng dẫn: <br>&emsp; + Sử dụng draw.io với AWS icons <br>&emsp; + Best practices trong việc thiết kế architecture diagram <br>&emsp; + Cách thể hiện flow và connections giữa các services <br> - Ghi nhận sự cố: **AWS sập tại us-east-1**, ảnh hưởng nghiêm trọng đến nhiều hệ thống toàn cầu | 20/10/2025 | 20/10/2025 | [AWS Study Group](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=2) |
| 3 | - Tiếp tục **vẽ và chỉnh sửa architecture** cho dự án: <br>&emsp; + Dựa trên pre-architecture đã lên ý tưởng <br>&emsp; + Bổ sung các components mới <br>&emsp; + Tối ưu hóa flow và connections <br> - **Họp với nhóm về direction** cho dự án: <br>&emsp; + Xác định mục tiêu chính của chatbot <br>&emsp; + Định nghĩa scope và tính năng <br>&emsp; + Phân tích use cases | 21/10/2025 | 21/10/2025 | [Notion - Pre Architecture](https://www.notion.so/pre-archi-28fd23b23efb808b978dfb3f9a20389d) <br> [Notion - Directions](https://www.notion.so/Directions-295d23b23efb80bb9500e5cb3222414c) |
| 4 | - Nghiên cứu **cơ chế Text-to-SQL**: <br>&emsp; + Đọc paper: "HEXGEN-FLOW: Optimizing LLM Inference Request Scheduling for Agentic Text-to-SQL" <br>&emsp; + Hiểu cách LLM chuyển đổi natural language thành SQL queries <br>&emsp; + Phân tích flow xử lý và optimization techniques <br> - **Họp team về tương tác giữa chatbot với database**: <br>&emsp; + Làm rõ cách chatbot xử lý Text-to-SQL <br>&emsp; + Giới hạn quyền của chatbot (READ-ONLY vs READ-WRITE) <br>&emsp; + Bảo mật thông tin nhạy cảm <br>&emsp; + Kiểm soát các câu lệnh nguy hiểm (DROP, DELETE, UPDATE) | 22/10/2025 | 22/10/2025 | [Paper - HEXGEN-FLOW](https://arxiv.org/pdf/2505.05286) <br> Notion Meeting Notes |
| 5 | - **Ôn tập kiến thức nền tảng AWS**: <br>&emsp; + Review các dịch vụ đã học (EC2, RDS, S3, Lambda, v.v.) <br>&emsp; + Ôn tập best practices và use cases <br>&emsp; + Chuẩn bị cho bài kiểm tra định kỳ | 23/10/2025 | 23/10/2025 | [Cloud Journey - AWS Study Group](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được tuần 7:

* Nắm vững cách **vẽ kiến trúc AWS** sử dụng draw.io 

* **Cải thiện pre-architecture** cho dự án chatbot

* Xác định rõ **direction và scope** cho dự án:
  * Mục tiêu và tính năng chính của chatbot
  * Use cases cụ thể
  * Phạm vi triển khai giai đoạn đầu

* Hiểu sâu về **cơ chế Text-to-SQL**:
  * Cách LLM chuyển đổi natural language thành SQL queries
  * Flow xử lý và optimization techniques từ paper HEXGEN-FLOW
  * Các thách thức trong việc parse và generate SQL chính xác

* Phân tích chi tiết **vấn đề bảo mật database** khi chatbot tương tác với DB:
  * Xác định cần giới hạn quyền của chatbot (READ-ONLY hay có cho phép WRITE)
  * Cách kiểm soát các câu lệnh nguy hiểm (DROP, DELETE, UPDATE không hợp lệ)
  * Bảo vệ thông tin nhạy cảm và ngăn chặn SQL injection
  * Thiết kế permission model phù hợp

* Ghi nhận và theo dõi **sự cố AWS outage tại us-east-1**