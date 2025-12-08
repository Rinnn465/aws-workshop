---
title: "Blog 1"
date: "2025-11-25"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Các Biện pháp Tốt nhất về Bảo mật và Bảo vệ Dữ liệu với Veeam trên AWS

Tác giả: Desmond Lai Xu và Vishwajeeth Venkatesh | Ngày 11 Tháng 3, 2025 | trên [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Bedrock Agents](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-agents/), [Best Practices](https://aws.amazon.com/blogs/machine-learning/category/post-types/best-practices/), [Generative AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/generative-ai/), [Technical How-to](https://aws.amazon.com/blogs/machine-learning/category/post-types/technical-how-to/), [Thought Leadership](https://aws.amazon.com/blogs/machine-learning/category/post-types/thought-leadership/) [Permalink](https://aws.amazon.com/blogs/machine-learning/dynamic-text-to-sql-for-enterprise-workloads-with-amazon-bedrock-agents/) | [Comments](https://aws.amazon.com/blogs/apn/data-protection-and-security-best-practices-with-veeam-on-aws/#Comments) [| Share](https://aws.amazon.com/blogs/apn/data-protection-and-security-best-practices-with-veeam-on-aws/)



### 

Bảo vệ thông tin nhạy cảm là điều tối quan trọng đối với mọi tổ chức. Với sự gia tăng khối lượng dữ liệu từ hàng trăm terabyte lên đến petabyte, bao gồm Thông tin Nhận dạng Cá nhân (PII) nhạy cảm, các tổ chức phải tuân thủ các yêu cầu quy định nghiêm ngặt liên quan đến an ninh dữ liệu. Các tổ chức cần bảo vệ dữ liệu và cảnh quan CNTT của mình khỏi các cấu hình sai, lỗi của con người và các mối đe dọa mạng đang phát triển như ransomware và các lỗ hổng trong môi trường. Điều này khiến các tổ chức dễ bị tổn thất về tài chính, danh tiếng và hoạt động. Các thách thức phổ biến của khách hàng bao gồm:

* **Sao lưu dữ liệu không an toàn:** Các bản sao lưu được cấu hình kém sẽ để lại những lỗ hổng trong kế hoạch khôi phục sau sự cố  
* **Lỗ hổng dữ liệu trong quá trình truyền tải:** Mã hóa không đúng cách trong quá trình truyền tải khiến dữ liệu dễ bị chặn/đánh cắp.  
* **Quản lý IAM (Quản lý Danh tính và Truy cập) kém:** Do cấu hình danh tính và quyền truy cập bị sai.  
* **Mã độc tống tiền (Ransomware) nhắm vào các bản sao lưu:** Thông thường trong các cuộc tấn công ransomware, kho lưu trữ sao lưu là mục tiêu đầu tiên.

Những mối lo ngại này nhấn mạnh nhu cầu cấp thiết về việc bảo vệ dữ liệu mạnh mẽ và các chiến lược **an ninh mạng bền vững** hiệu quả để giảm thiểu rủi ro và đảm bảo tuân thủ.

![Ransomware Statistics](/images/3-BlogsTranslated/Blog1/image1.png)

## **Tổng quan về các biện pháp tốt nhất để Bảo mật dữ liệu**

Khi triển khai trên **đám mây AWS (AWS cloud)**, việc hiểu rõ [**Mô hình Trách nhiệm Chung của AWS (AWS Shared Responsibility Model)**](https://aws.amazon.com/compliance/shared-responsibility-model/) là rất quan trọng. Mô hình này phân định sự phân chia trách nhiệm bảo mật giữa AWS và khách hàng. Trong khi AWS quản lý **an ninh của cơ sở hạ tầng đám mây**, khách hàng chịu trách nhiệm bảo mật **dữ liệu của họ bên trong đám mây**. Điều này bao gồm việc triển khai các biện pháp quản lý danh tính và truy cập, mã hóa, và bảo mật mạng phù hợp.

Các biện pháp tốt nhất trong việc bảo mật dữ liệu của bạn bao gồm:

* **Thực hiện các chiến lược sao lưu nhiều lớp và được tăng cường bảo mật (hardened):** Đảm bảo các bản sao lưu được mã hóa và cô lập về mặt logic khỏi internet công cộng, tránh tiếp xúc và rủi ro.  
* **Mã hóa dữ liệu đang truyền tải và dữ liệu tĩnh:** Áp dụng các tiêu chuẩn cho dữ liệu đang truyền và dữ liệu được lưu trữ.  
* **Tăng cường các giao thức IAM (Quản lý Danh tính và Truy cập):** Thực hiện nguyên tắc **đặc quyền tối thiểu**, **xác thực đa yếu tố (MFA)**, và kiểm tra định kỳ.  
* **Bảo vệ khỏi Ransomware và cô lập bản sao lưu:** Triển khai các kho lưu trữ **bất biến** và cô lập dữ liệu sao lưu.

**Veeam** hỗ trợ khách hàng tuân thủ các quy định và khuôn khổ khu vực, địa phương và ngành nghề, bao gồm ([Cloud Act](https://aws.amazon.com/compliance/cloud-act/), [HIPAA](https://aws.amazon.com/compliance/hipaa-compliance/), [NIST](https://aws.amazon.com/compliance/nist/), [IRAP](https://aws.amazon.com/compliance/irap/), [MTCS Tier 3](https://aws.amazon.com/compliance/aws-multitiered-cloud-security-standard-certification), [OSPAR](https://aws.amazon.com/compliance/OSPAR/), [ISO 20000](https://aws.amazon.com/compliance/iso-20000-faqs/), và [nhiều quy định khác](https://aws.amazon.com/compliance/programs/)). Veeam thực hiện điều này bằng cách tích hợp liền mạch với các cơ chế do AWS cung cấp và các giải pháp có sẵn (out-of-the-box), cho phép khách hàng bảo mật môi trường đám mây AWS của họ một cách hiệu quả.

**Triển khai và Cấu hình Veeam Backup trên AWS**

Để đảm bảo dữ liệu của khách hàng được an toàn và bảo vệ trước các rủi ro tiềm ẩn, việc triển khai Veeam trên AWS cần tuân thủ các phương pháp bảo mật tốt nhất đã được thiết lập. Trong các phần tiếp theo, chúng ta sẽ tìm hiểu cách Veeam tích hợp các phương pháp này để giảm thiểu các mối đe dọa bảo mật, đảm bảo tuân thủ các tiêu chuẩn ngành và giảm thiểu rủi ro cho khách hàng.

## **1\. Tính bất biến của kho lưu trữ** 

Lưu trữ dữ liệu ở trạng thái không thể sửa đổi sau khi được tạo. Điều này đảm bảo tính toàn vẹn và độ bền của dữ liệu để đáp ứng các yêu cầu kiểm toán và tuân thủ bằng cách bảo vệ các bản ghi lịch sử và giao dịch, đảm bảo dữ liệu không thể bị xóa hoặc ghi đè trong một khoảng thời gian lưu giữ cụ thể.

**Triển khai và Tích hợp bởi Veeam**

Veeam Backup cho AWS cho phép bảo vệ dữ liệu được lưu trữ trong các kho lưu trữ sao lưu khỏi việc bị xóa bằng cách làm cho dữ liệu trở nên bất biến cho đến khi đạt được thời gian lưu giữ mong muốn. Veeam Backup sử dụng [Amazon Simple Storage Service (S3) Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html) để ngăn chặn việc xóa hoặc sửa đổi dữ liệu sao lưu dựa trên các chính sách lưu giữ. Trong chế độ tuân thủ, dữ liệu không thể bị can thiệp hoặc xóa bởi bất kỳ người dùng nào, kể cả người dùng gốc của tài khoản AWS, giúp bảo vệ chống lại ransomware và các hành động độc hại. Để biết chi tiết cấu hình, hãy tham khảo [hướng dẫn cấu hình tính bất biến trên tài liệu của Veeam](https://helpcenter.veeam.com/docs/vbaws/guide/immutability.html?ver=80).

![](/images/3-BlogsTranslated/Blog1/image2.png)

## **2\. Giảm thiểu Phạm vi Ảnh hưởng / Cô lập (Reducing Blast Radius / Isolation)**

Việc **cô lập** dữ liệu, cơ sở hạ tầng và ứng dụng một cách vật lý và logic sẽ giảm thiểu tác động của các sự cố. Bằng cách **chia nhỏ** dữ liệu và khối lượng công việc, các tổ chức có thể phân đoạn quyền truy cập tốt hơn và **thu hẹp bề mặt tấn công** , khiến kẻ tấn công khó di chuyển ngang hơn. Các môi trường cô lập cho phép các tổ chức xác định nhanh chóng nguồn gốc của vấn đề và áp dụng các giải pháp có mục tiêu mà không ảnh hưởng đến các phần khác của hệ thống.

## **Triển khai và Tích hợp bởi Veeam**

**Veeam** cho phép bạn tạo một **tài khoản sao lưu riêng biệt** để triển khai toàn bộ cơ sở hạ tầng sao lưu.

Việc này cũng có thể được triển khai ở một [**AWS Region**](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) **riêng biệt** để tăng cường tính **dự phòng**. Điều này đảm bảo tính khả dụng nếu tài khoản AWS của bạn bị xâm phạm, đồng thời giải quyết mọi vấn đề về tính sẵn sàng ở cấp độ địa lý (geo-level availability).

![Multi-Account Architecture](/images/3-BlogsTranslated/Blog1/image3.png)

## **3\. Mã hóa Mọi nơi (Encryption Everywhere)**

Việc bảo vệ dữ liệu **đang truyền tải** và **dữ liệu tĩnh** khiến dữ liệu trở nên không thể đọc được đối với những **tác nhân xấu**, cả bên trong lẫn bên ngoài. Nhiều tiêu chuẩn quy định và khuôn khổ tuân thủ yêu cầu [mã hóa dữ liệu để bảo vệ thông tin](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec-dataprot.html). Bằng cách mã hóa dữ liệu theo các yêu cầu này, các tổ chức có thể đảm bảo **tuân thủ** và tránh các hình phạt hoặc vấn đề pháp lý tiềm ẩn.

## **Triển khai và Tích hợp bởi Veeam**

Các **bucket Amazon S3** được mã hóa theo mặc định bằng cách sử dụng các khóa do Amazon S3 quản lý (**SSE-S3**), cung cấp bảo mật dữ liệu cơ bản. Để tăng cường bảo vệ, **Veeam Backup for AWS** cho phép người dùng mã hóa dữ liệu sao lưu được lưu trữ trong các kho lưu trữ thông qua các cơ chế mã hóa riêng của Veeam.

Hơn nữa, Veeam mở rộng bảo mật này bằng cách hỗ trợ mã hóa [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/) cho các volume của [Amazon Elastic Cloud Compute (Amazon EC2)](https://aws.amazon.com/pm/ec2/) và [Amazon Relation Database Service (Amazon RDS)](https://aws.amazon.com/rds/), hệ thống tệp [Amazon Elastic File System (Amazon EFS)](https://aws.amazon.com/efs/), hệ thống tệp [Amazon FSx](https://aws.amazon.com/fsx/) , các bảng [Amazon DynamoDB](https://aws.amazon.com/dynamodb/), và các ảnh chụp nhanh (snapshots) gốc của đám mây. Veeam sử dụng **Tiêu chuẩn Mã hóa Nâng cao (AES) 256-bit** cho quy trình mã hóa của mình, đảm bảo khả năng bảo vệ mạnh mẽ.

**Veeam Backup for AWS** sử dụng các **AWS KMS** và **CMK** để mã hóa dữ liệu sao lưu ở trạng thái tĩnh (**at rest**) và **đang truyền tải (in transit)**. Quá trình mã hóa bảo mật các ảnh chụp nhanh ở cấp độ khối (**block level**) trước khi gắn vào các phiên bản worker và duy trì sự bảo vệ trong suốt quy trình làm việc sao lưu S3, đảm bảo an toàn và tuân thủ dữ liệu.

Veeam tích hợp liền mạch với các [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/), đảm bảo rằng chỉ các vai trò được ủy quyền mới có thể truy cập hoặc quản lý các bản sao lưu đã được mã hóa. Bằng cách thực thi mã hóa trên tất cả các điểm dữ liệu, Veeam đơn giản hóa việc quản lý các chính sách mã hóa đồng thời củng cố tính bảo mật tổng thể của dữ liệu sao lưu.

![Encryption Architecture](/images/3-BlogsTranslated/Blog1/image4.png)

## **4\. Quản lý Danh tính và Truy cập (Identity and Access Management \- IAM)**

Việc cấu hình **IAM** chính xác đảm bảo rằng **đúng người dùng** truy cập **đúng dữ liệu** vào **đúng thời điểm**, với [**mức cấp phép tối thiểu**](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec_permissions_least_privileges.html) để thực hiện một tác vụ. Điều này cung cấp khả năng kiểm soát tập trung và khả năng hiển thị về hoạt động và quyền truy cập của người dùng trên các dịch vụ và tài nguyên AWS, cho phép các tổ chức giám sát hành vi người dùng, phát hiện hoạt động đáng ngờ và phản ứng với các sự cố bảo mật theo thời gian thực.

## **Triển khai và Tích hợp bởi Veeam**

**Veeam** cho phép bạn tạo các **vai trò IAM chi tiết (granular IAM roles)** để thực hiện các hoạt động sao lưu và khôi phục trong nhiều tài khoản AWS. Veeam thực thi nguyên tắc **đặc quyền tối thiểu (least privileged access)**, chỉ cấp cho người dùng và hệ thống mức truy cập tối thiểu cần thiết để thực hiện các tác vụ cần thiết của họ, làm giảm thiệt hại tiềm tàng trong trường hợp bị xâm phạm.

Veeam tích hợp với các nhà cung cấp **đăng nhập một lần (single sign-on)** và **xác thực đa yếu tố (multi-factor authentication)** để tăng cường bảo mật. Việc gán vai trò chi tiết sẽ giảm thiểu rủi ro bị xâm phạm trong các cuộc kiểm tra bảo mật AWS. Để biết chi tiết, vui lòng tham khảo tài liệu [**Veeam Backup for AWS IAM Permissions**](https://helpcenter.veeam.com/docs/vbaws/guide/system_requirements_permissions.html?ver=80) để có thêm thông tin.

## **5\. Kết nối Riêng tư Đầu cuối (End-to-End Private Connectivity)**

Việc triển khai mạng riêng tư giảm thiểu rủi ro bảo mật bằng cách ngăn chặn sự tiếp xúc với **internet công cộng**, bảo vệ chống lại việc nghe lén và chặn dữ liệu, đồng thời cải thiện hiệu suất và độ tin cậy của mạng.

Các kết nối chuyên dụng hoặc VPN cung cấp **băng thông có thể dự đoán được**, **độ trễ thấp hơn** và **thông lượng cao hơn**, đảm bảo hiệu suất tối ưu cho các ứng dụng và khối lượng công việc quan trọng.

## **Triển khai và Tích hợp bởi Veeam**

**Veeam** hỗ trợ triển khai **cơ sở hạ tầng sao lưu trong môi trường riêng tư** để đảm bảo các thành phần sao lưu cốt lõi được bảo mật và không có các điểm cuối (endpoints) hướng ra công chúng. Veeam cho phép bạn triển khai [**thiết bị sao lưu trong một môi trường riêng tư**.](https://helpcenter.veeam.com/docs/vbaws/guide/appliance_in_private.html?ver=80)

Ngoài ra, Veeam có thể kích hoạt chức năng triển khai mạng riêng tư, cho phép giao tiếp với **Amazon S3** thông qua [**các điểm cuối giao diện Amazon S3 riêng tư**](https://docs.aws.amazon.com/AmazonS3/latest/userguide/privatelink-interface-endpoints.html). Veeam cho phép bạn triển khai các **[worker trong môi trường riêng tư](https://helpcenter.veeam.com/docs/vbaws/guide/worker_instances_in_private.html?ver=80)** mà không cần gán **IPV4 công cộng**, đảm bảo luồng lưu lượng sao lưu được bảo mật.

![Private Connectivity Architecture](/images/3-BlogsTranslated/Blog1/image5.png)

Nếu bạn đang tìm cách triển khai **Veeam Backup for AWS** trong môi trường riêng tư và cần hướng dẫn, Veeam cung cấp một **kịch bản tự động hóa** để giúp bạn bắt đầu.

## **Kết luận**

**Veeam®**, công ty dẫn đầu thị trường toàn cầu về bảo vệ dữ liệu và khôi phục sau tấn công ransomware, đang thực hiện sứ mệnh trao quyền cho các tổ chức không chỉ **phục hồi** sau sự cố mất hoặc ngừng hoạt động dữ liệu mà còn **phát triển vượt bậc**. Với Veeam, các tổ chức đạt được **khả năng phục hồi triệt để** thông qua bảo mật dữ liệu, khôi phục dữ liệu và tự do dữ liệu cho các môi trường **hybrid cloud** của họ.

**Nền tảng Dữ liệu Veeam** cung cấp một giải pháp duy nhất cho các môi trường **đám mây**, **ảo hóa**, **vật lý**, **SaaS** và **Kubernetes**, mang lại sự an tâm cho các nhà lãnh đạo CNTT và bảo mật rằng các ứng dụng và dữ liệu của họ luôn được bảo vệ và sẵn sàng. Có trụ sở chính tại Columbus, Ohio, với các văn phòng tại hơn 30 quốc gia, Veeam bảo vệ hơn **450.000 khách hàng** trên toàn thế giới, bao gồm **73%** trong số **2000 công ty lớn nhất toàn cầu (Global 2000\)**, những người đã tin tưởng Veeam để duy trì hoạt động kinh doanh của họ.

**Veeam trên AWS** cung cấp khả năng bảo vệ dữ liệu và khôi phục sau tấn công ransomware toàn diện thông qua các biện pháp tốt nhất về bảo mật, được tăng cường bởi cơ sở hạ tầng có khả năng **mở rộng** của AWS cho các khả năng sao lưu và khôi phục sau thảm họa.

Quan hệ đối tác **Veeam-AWS** tận dụng **S3** và **Glacier Deep Archive** để bảo vệ dữ liệu an toàn, **hiệu quả về chi phí** và khôi phục nhanh chóng. Bằng cách tuân thủ các biện pháp tốt nhất của AWS, Veeam đảm bảo an ninh dữ liệu, khả năng phục hồi và tuân thủ các quy định, đồng thời bảo vệ khỏi ransomware và mất mát dữ liệu.
