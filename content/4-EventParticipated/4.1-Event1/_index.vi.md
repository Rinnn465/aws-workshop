---
title: "Event 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---


# Tổng kết từ sự kiện: "AWS Cloud Mastery Series #1 - AI/ML/GenAI trên AWS"

### Định hướng chương trình

- Khám phá toàn cảnh AI/ML/GenAI capabilities trên AWS và phương pháp ứng dụng vào các tình huống thực tế.

### Danh Sách Diễn Giả

- **Lâm Tuấn Kiệt** – Sr DevOps Engineer, FPT Software  
- **Danh Hoàng Hiếu Nghị** – AI Engineer, Renova Cloud  
- **Đinh Lê Hoàng Anh** – Cloud Engineer Trainee, First Cloud AI Journey  
- **Văn Hoàng Kha** – Community Builder

### Nội Dung Nổi Bật

## 1. Generative AI với Amazon Bedrock Platform

**Foundation Models (FMs):**  
AWS cung cấp bộ sưu tập các mô hình nền tảng được quản lý đầy đủ từ các nhà cung cấp AI hàng đầu (Anthropic, OpenAI, Meta, v.v.), cho phép tùy biến cho đa dạng tác vụ mà không cần training models từ đầu.

**Prompt Engineering techniques:**  
Nắm vững cách điều khiển models thông qua các chiến lược prompting khác nhau:
  + **Zero-shot:** Model chỉ nhận task description, không có examples.  
  + **Few-shot:** Model được cung cấp một số examples để học theo.  
  + **Chain-of-Thought:** Khuyến khích model trình bày reasoning steps để tăng độ chính xác.

**Retrieval Augmented Generation (RAG):**  
Nâng cao chất lượng output bằng cách tiêm external knowledge:
  + **R – Retrieval:** Truy xuất dữ liệu liên quan từ knowledge store.  
  + **A – Augmentation:** Bổ sung dữ liệu này làm context trong prompt.  
  + **G – Generation:** Model tạo ra câu trả lời có căn cứ và chính xác hơn.  
  + **Applications:** Context-aware chatbots, enhanced search, real-time data summarization.

**Amazon Titan Embeddings:**  
Mô hình embedding nhỏ gọn, chuyển đổi text thành dense vectors phục vụ similarity search và RAG workflows, hỗ trợ multilingual.

**AWS AI Services:** Các API AI ready-to-use:
  - Rekognition – Image/Video analysis  
  - Translate – Language translation  
  - Textract – Document text & layout extraction  
  - Transcribe – Speech-to-text conversion  
  - Polly – Text-to-speech synthesis  
  - Comprehend – Natural language processing  
  - Kendra – Enterprise intelligent search  
  - Lookout – Anomaly detection  
  - Personalize – Recommendation engines  

**Demo highlight:**  
Ứng dụng nhận diện khuôn mặt AMZPhoto minh họa cách tích hợp AI services vào user-facing products.

---

## 2. Amazon Bedrock AgentCore – Framework cho Production-Ready AI Agents

Một framework mới cho phép teams vận hành AI agents một cách đáng tin cậy ở quy mô lớn:
  - Execute và scale agent workflows một cách an toàn  
  - Quản lý long-term memory  
  - Cấp fine-grained identity & access control  
  - Tích hợp với các tools như Browser Tool, Code Interpreter, Memory Store  
  - Cung cấp observability và auditing capabilities  
  - Hỗ trợ các popular agent frameworks (CrewAI, LangGraph, LlamaIndex, OpenAI Agents SDK, v.v.)

---

### Những điểm rút ra

- **Bedrock làm trung tâm GenAI platform:** Truy cập dễ dàng nhiều FMs tại một điểm.  
- **Prompting + RAG như công cụ customization:** Cải thiện model relevance bằng context và examples.  
- **Embeddings cho intelligent search:** Titan Embeddings tăng retrieval accuracy cho knowledge-driven applications.  
- **Pre-built models rút ngắn development cycle:** Không cần xây dựng mọi thứ từ đầu.  
- **AgentCore giảm deployment complexity:** Xử lý scaling, memory, identity và monitoring cho agentic systems.

---

### Ứng dụng thực tế

- Các concepts từ session (đặc biệt RAG và AgentCore) có thể align trực tiếp với các internal projects trong tương lai liên quan đến GenAI-powered features.
- Hiểu rõ AWS AI services giúp lựa chọn đúng tools cho các application needs khác nhau, tăng tốc development cycles.
- Kiến thức về prompt engineering có thể áp dụng để cải thiện performance của AI models trong nhiều scenarios.

### Trải nghiệm sự kiện

Tham gia workshop **"GenAI-powered App-DB Modernization"** mang lại trải nghiệm vô cùng giá trị, cung cấp cái nhìn comprehensive về modernization approach cho applications và databases sử dụng các công cụ và phương pháp hiện đại. Những highlights đáng nhớ:

- Đạt top 5 trong Kahoot Quiz cuối event và được chụp ảnh cùng speakers.  
- Hình thành collaborative group nhỏ mang tên **"Mèo Cam Đeo Khăn"**, kết hợp members từ "The Ballers" và "Vinhomies".


#### Hình ảnh từ sự kiện
![Event1-1](/images/4-EventParticipated/event1-1.jpg)
![Event1-2](/images/4-EventParticipated/event1=2.jpg)
![Event1-3](/images/4-EventParticipated/event1-3.jpg)
