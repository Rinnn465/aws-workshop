---
title: "Blog 2"
date: "2025-11-25"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---


# Triển khai hiệu quả các chính sách kiểm soát tài nguyên trong môi trường đa tài khoản

Tác giả: Tatyana Yatskevich và Harsha Sharma | Ngày 26 Tháng 3, 2025 | trên [Announcements](https://aws.amazon.com/blogs/security/category/post-types/announcements/), [Intermediate (200)](https://aws.amazon.com/blogs/security/category/learning-levels/intermediate-200/), [Security, Identity, & Compliance](https://aws.amazon.com/blogs/security/category/security-identity-compliance/), [Technical How-to](https://aws.amazon.com/blogs/security/category/post-types/technical-how-to/) | [Permalink](https://aws.amazon.com/blogs/security/effectively-implementing-resource-controls-policies-in-a-multi-account-environment/) | [Comments](https://aws.amazon.com/blogs/security/effectively-implementing-resource-controls-policies-in-a-multi-account-environment/#Comments) | [Share](https://aws.amazon.com/vi/blogs/security/effectively-implementing-resource-controls-policies-in-a-multi-account-environment/#)

Mọi tổ chức đều cố gắng trao quyền cho các đội nhóm thúc đẩy đổi mới đồng thời bảo vệ dữ liệu và hệ thống của họ khỏi sự truy cập ngoài ý muốn. Đối với các tổ chức có hàng ngàn tài nguyên [**Amazon Web Services (AWS)**](https://aws.amazon.com/) trải rộng trên nhiều tài khoản, các hàng rào bảo vệ quyền hạn trên toàn tổ chức có thể giúp duy trì các cấu hình an toàn và tuân thủ.

Ví dụ, một số dịch vụ AWS hỗ trợ [**chính sách dựa trên tài nguyên**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html), có thể được sử dụng để cấp quyền cho các danh tính thực hiện hành động trên các tài nguyên mà chúng được đính kèm. Với việc quản lý các chính sách dựa trên tài nguyên thường được ủy quyền cho chủ sở hữu ứng dụng, các đội bảo mật trung tâm sử dụng các hàng rào bảo vệ quyền hạn để giúp đảm bảo rằng các cấu hình sai sót tiềm ẩn không dẫn đến truy cập ngoài ý muốn vào các tài nguyên này.

Trong bài đăng này, chúng tôi thảo luận về cách bạn có thể sử dụng [**chính sách kiểm soát tài nguyên (RCPs)**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps.html) để hạn chế truy cập vào tài nguyên một cách tập trung. Chúng tôi trình bày cách RCPs có thể giúp cải thiện tư thế bảo mật của bạn đồng thời cho phép các nhà phát triển có nhiều quyền tự do hơn trong việc quản lý tài nguyên của họ, từ đó giảm thiểu sự ma sát giữa các đội bảo mật trung tâm và đội ứng dụng. Sử dụng một trường hợp sử dụng mẫu, chúng tôi sẽ làm rõ các cân nhắc chính để thiết kế và triển khai hiệu quả RCPs trong tổ chức của bạn ở quy mô lớn.

Nếu bạn chưa quen với RCPs, chúng tôi khuyên bạn nên bắt đầu với bài viết [**Giới thiệu chính sách kiểm soát tài nguyên (RCPs), một loại chính sách ủy quyền mới trong AWS Organizations**](https://aws.amazon.com/blogs/aws/introducing-resource-control-policies-rcps-a-new-authorization-policy/), bài viết cung cấp phần giới thiệu về RCPs và vai trò của chúng trong chiến lược bảo mật của bạn.

## **Hành trình Triển khai RCP**

RCPs là một loại chính sách ủy quyền trong [AWS Organizations](https://aws.amazon.com/organizations/). RCPs hoạt động cùng với [**SCPs** (Chính sách Kiểm soát Dịch vụ)](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) để giúp [thiết lập các hàng rào bảo vệ quyền hạn](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-permissions-guardrails) trên nhiều tài khoản trong tổ chức của bạn. Để hiểu sự khác biệt và các trường hợp sử dụng của chúng, hãy tham khảo bài viết [*General use cases for SCPs and RCPs*](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_authorization_policies.html#scps-rcps-general-use-cases) (Các trường hợp sử dụng chung cho SCPs và RCPs) và [*Enforcing enterprise-wide preventive controls with AWS Organizations*](https://aws.amazon.com/blogs/mt/enforcing-enterprise-wide-preventive-controls-with-aws-organizations/) (Thực thi các biện pháp kiểm soát phòng ngừa trên toàn doanh nghiệp với AWS Organizations).

![Các giai đoạn triển khai](/images/3-BlogsTranslated/Blog2/image1.png)

*Hình 1: Các giai đoạn triển khai các hàng rào bảo vệ quyền hạn*

Chúng tôi khuyên bạn nên triển khai các hàng rào bảo vệ quyền hạn, bao gồm RCPs, bằng quy trình lặp lại sau đây, gồm năm giai đoạn:

1. Kiểm tra các mục tiêu kiểm soát bảo mật của bạn  
2. Thiết kế các hàng rào bảo vệ quyền hạn  
3. Dự đoán các tác động tiềm ẩn  
4. Triển khai các hàng rào bảo vệ quyền hạn  
5. Giám sát các hàng rào bảo vệ quyền hạn

## **Giai đoạn 1: Kiểm tra các Mục tiêu Kiểm soát Bảo mật của bạn**

Bước đầu tiên trong việc triển khai RCPs là xác định các lĩnh vực mà RCPs có thể giúp cải thiện bảo mật của bạn hoặc tối ưu hóa việc triển khai kiểm soát cho các mục tiêu kiểm soát bảo mật cụ thể của tổ chức bạn.

![Kịch bản đơn giản](/images/3-BlogsTranslated/Blog2/image2.png)

*Hình 2: Kịch bản đơn giản mô tả một danh tính đáng tin cậy truy cập một vai trò IAM*

Một cách để đạt được mục tiêu kiểm soát này là tuân theo nguyên tắc đặc quyền tối thiểu và đảm bảo rằng chính sách tin cậy của vai trò, tức là chính sách dựa trên tài nguyên được đính kèm vào vai trò IAM, chỉ cho phép các danh tính yêu cầu quyền truy cập đó.

![Chính sách tin cậy](/images/3-BlogsTranslated/Blog2/image3.png)

*Ví dụ về chính sách tin cậy cấp quyền cho Role A trong Account A được assume Role B trong Account B*

Giả sử công ty của bạn đã bắt đầu mở rộng quy mô sử dụng đám mây đến mức đội ngũ bảo mật trung tâm của bạn hiện phải đạt được cùng một mục tiêu kiểm soát với hàng trăm vai trò IAM được phân bổ trên nhiều tài khoản AWS.

![Hạn chế truy cập](/images/3-BlogsTranslated/Blog2/image4.png)

*Hình 3: Hạn chế truy cập bằng cách quản lý từng chính sách tin cậy của vai trò IAM riêng lẻ*

## **Giai đoạn 2: Thiết kế các Hàng rào Bảo vệ Quyền hạn**

Các đội ngũ bảo mật trung tâm có thể triển khai các hàng rào bảo vệ quyền hạn bằng cách tạo một **RCP** (Chính sách Kiểm soát Tài nguyên) để chặn truy cập bên ngoài vào các vai trò IAM một cách tập trung.

Mặc dù việc thêm câu lệnh **RestrictAccessToMyOrg** vào các chính sách tin cậy có thể được tự động hóa, RCPs (Chính sách Kiểm soát Tài nguyên) có thể đơn giản hóa rất nhiều việc thực thi các kiểm soát thô bằng cách chỉ định các chính sách quyền hạn trong **Resource Control Policies** và áp dụng chúng trên các OU hoặc tài khoản khác nhau. Điều này làm giảm nhu cầu cập nhật các chính sách dựa trên tài nguyên trên nhiều tài nguyên riêng lẻ, do đó tăng tính hiệu quả về vận hành. Hãy xem xét ví dụ mẫu dưới đây, minh họa một RCP được áp dụng vào một OU trong tổ chức AWS Organizations của bạn. Hãy lưu ý rằng RCP chỉ cần liên kết với (attached to) OU này một lần. Sau đó, nó sẽ được thực thi tự động trên tất cả tài nguyên hiện tại và tương lai trong các tài khoản thuộc về OU đó.

![Hình 3: RCP được gắn vào một OU](/images/3-BlogsTranslated/Blog2/image6.png)

RCPs cung cấp tính linh hoạt trong việc tùy chỉnh các **hàng rào bảo vệ quyền hạn** theo các cấp độ khác nhau của tổ chức để đáp ứng các nhu cầu riêng biệt của các đơn vị. Hình 4 minh họa một cấu trúc tổ chức mẫu trong đó các RCP với tính cụ thể và khắt khe tăng dần được áp dụng khi bạn đi theo cấu trúc phân cấp từ gốc xuống. Ví dụ: bạn có thể cấm quyền truy cập bên ngoài vào các vai trò IAM của mình ở cấp gốc. Sau đó, trên một OU mà các nhóm sử dụng AWS CodeBuild để tích hợp liên tục, bạn có thể áp dụng các kiểm soát bổ sung để hạn chế khả năng chia sẻ các dự án CodeBuild với các thực thể bên ngoài tổ chức của bạn.

![Hình 4: Một tổ chức mẫu với các RCP được áp dụng ở nhiều cấp độ](/images/3-BlogsTranslated/Blog2/image7.png)

Ví dụ: nếu bạn cần loại trừ **Account A** (một tài khoản thử nghiệm) khỏi các kiểm soát của mình nhưng vẫn muốn áp dụng chúng trong toàn bộ **Dev OU**, bạn có thể đơn giản hóa chiến lược triển khai của mình bằng cách đính kèm một RCP vào **Dev OU** với một câu lệnh duy nhất giúp loại trừ **Account A** khỏi bất kỳ control nào.

![Hình sau minh họa ngoại lệ cho Account A](/images/3-BlogsTranslated/Blog2/image8.png)

Một cách tiếp cận khác là sử dụng **resource tags** để cấp ngoại lệ cho các đối tác đáng tin cậy (trusted partner). Ví dụ: giả sử bạn đang sử dụng một công cụ Cloud Security Posture Management **(CSPM)** bên ngoài yêu cầu truy cập vào các vai trò IAM của bạn. Ngoài việc xác minh và thêm tài khoản CSPM vào RCPs, bạn có thể sử dụng **thẻ tài nguyên (resource tags)** như một cơ chế để cấp các ngoại lệ như được thể hiện trong **Hình 5**. Sau đó, bạn có thể cấu hình một **quy trình cấp phép** để giúp đảm bảo rằng một sự kiện được ghi nhận khi các nhóm gắn thẻ này.

![Hình 5: Minh họa việc cấp ngoại lệ cho các đối tác đáng tin cậy](/images/3-BlogsTranslated/Blog2/image9.png)

RCP mẫu sau sử dụng khóa ngữ cảnh **aws:PrincipalAccount** để cấp ngoại lệ cho một tập hợp tài khoản đáng tin cậy cụ thể. Ngoài ra, nó sử dụng **aws:ResourceTag** trên vai trò IAM được đảm nhận để cấp các ngoại lệ cho các đối tác khác. Điều này có nghĩa là các chính sách này có thể bao gồm hai loại ngoại lệ khác nhau thông qua:

* ### **RestrictAccessToMyOrgExceptTaggedRoles:** Câu lệnh này giúp đảm bảo rằng các vai trò của bạn chỉ có thể được đảm nhận bởi các đối tượng thuộc về tổ chức của bạn hoặc bởi các đối tượng dịch vụ AWS (trừ khi vai trò đó được gắn thẻ **`partner-access-exception`** có giá trị là **`trusted-partner`**).

* ### **RestrictAccessForTaggedRoles:** Câu lệnh này hạn chế truy cập hơn nữa bằng cách giúp đảm bảo rằng các vai trò có thẻ **`partner-access-exception`** chỉ có thể được đảm nhận bởi các đối tượng thuộc về tài khoản đối tác đáng tin cậy của bạn.

![RCP mẫu sử dụng thẻ ngoại lệ](/images/3-BlogsTranslated/Blog2/image10.png)

Nếu bạn có một tập hợp tài nguyên đã biết rõ và được giới hạn chặt chẽ cần được loại trừ, bạn cũng có thể sử dụng thành phần chính sách IAM là [**`NotResource`**](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_notresource.html) để liệt kê các Tên Tài nguyên Amazon **(ARNs)** của các tài nguyên cần loại trừ khỏi kiểm soát.

Khi triển khai các quy trình ngoại lệ dựa trên thẻ, việc thiết lập kiểm soát chặt chẽ đối với việc quản lý thẻ là then chốt. Việc sửa đổi thẻ trái phép trên tài nguyên, đối tượng hoặc phiên có thể ảnh hưởng đến tư thế bảo mật của bạn bằng cách cho phép truy cập ngoài ý muốn. Bạn nên triển khai các biện pháp kiểm soát để giúp ngăn chặn việc thao túng thẻ trái phép. Ví dụ: SCP sau hạn chế việc sử dụng thẻ **`partner-access-exception`** chỉ đối với vai trò quản trị viên (**admin role**), để người dùng không được ủy quyền không thể thay đổi kiểm soát bằng cách đính kèm, gỡ bỏ hoặc sửa đổi thẻ này.

![SCP hạn chế việc quản lý thẻ partner-access-exception](/images/3-BlogsTranslated/Blog2/image11.png)

Bạn cũng nên đảm bảo rằng thẻ **`partner-access-exception`** không thể được truyền dưới [dạng thẻ phiên](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_session-tags.html) **(session tag)** khi các danh tính đảm nhận vai trò. Hãy xem mẫu [**RCP**](https://github.com/aws-samples/data-perimeter-policy-examples/blob/main/resource_control_policies/data_perimeter_governance_rcp.json) trong kho lưu trữ ví dụ về chính sách vùng biên dữ liệu.

![Cấu trúc tổ chức](/images/3-BlogsTranslated/Blog2/image5.png)

### Thiết kế để đạt được sự Xuất sắc trong việc Vận hành 

Một nền tảng then chốt để triển khai và vận hành hiệu quả các hàng rào bảo vệ quyền hạn như RCPs là tổ chức môi trường AWS của bạn bằng cách sử dụng nhiều tài khoản. Ranh giới tài khoản và việc đặt các khối lượng công việc một cách chiến lược trên các tài khoản đó cho phép bạn áp dụng các kiểm soát truy cập được tùy chỉnh phù hợp với độ nhạy cảm của dữ liệu và các yêu cầu truy cập cụ thể.

## **Giai đoạn 3: Dự đoán các Tác động Tiềm ẩn**

Trước khi triển khai RCPs, bạn cần phải hiểu tác động tiềm tàng của chúng đối với tổ chức của mình. Việc giới thiệu các chính sách mới hoặc sửa đổi các chính sách hiện có mà không có quy trình xác thực phù hợp có thể làm gián đoạn sự cân bằng giữa bảo mật và năng suất của bạn.

Hãy cân nhắc sử dụng AWS Identity and Access Management Access Analyzer để giám sát các quyền hạn hiệu quả trên các tài nguyên trong tổ chức của bạn.

## **Giai đoạn 4: Triển khai các Hàng rào Bảo vệ Quyền hạn**

Khi chuyển sang giai đoạn triển khai, hãy xem xét các yếu tố then chốt sau để thúc đẩy một quá trình triển khai suôn sẻ đồng thời nâng cao tư thế bảo mật của bạn.

### **Tự động hóa và Tích hợp Triển khai**

Sử dụng các pipeline hiện có của bạn để triển khai RCPs, tương tự như cách bạn làm với SCPs. Cách tiếp cận này sẽ giảm thiểu chi phí vận hành đồng thời duy trì tính nhất quán trong việc triển khai các kiểm soát của bạn.

### **Triển khai Từng bước** 

Tương tự như với SCPs, AWS đặc biệt khuyên không nên đính kèm RCPs trong môi trường sản xuất mà không thử nghiệm kỹ lưỡng tác động của các chính sách đó đối với tài nguyên trong tài khoản của bạn.

## **Giai đoạn 5: Giám sát các Hàng rào Bảo vệ Quyền hạn**

Cuối cùng, hãy thiết lập các quy trình giám sát để giúp đảm bảo rằng các biện pháp kiểm soát nhằm ngăn chặn truy cập bên ngoài vào tài nguyên của bạn hoạt động như mong đợi.

Ví dụ, bạn có thể sử dụng các phát hiện truy cập bên ngoài của IAM Access Analyzer để hiểu tác động của RCPs đối với quyền hạn tài nguyên. Thông tin này sẽ giúp bạn xác minh rằng RCPs được xây dựng theo đúng ý định của bạn và lập kế hoạch hành động khắc phục, nếu cần.

## **Kết luận**

Trong bài đăng này, chúng tôi đã thảo luận về cách triển khai hiệu quả các control truy cập thô trên các tài nguyên AWS ở quy mô lớn bằng cách sử dụng RCPs. Bạn có thể sử dụng cách tiếp cận theo từng giai đoạn được mô tả ở đây để đạt được các mục tiêu kiểm soát bảo mật của mình đồng thời giảm thiểu rủi ro làm gián đoạn các quy trình kinh doanh.

Hãy nhớ rằng RCPs, giống như SCPs, cung cấp một cơ chế mạnh mẽ để thực thi các kiểm soát thô trên nhiều tài khoản trong tổ chức của bạn. Chúng không thay thế các control đặc quyền tối thiểu của bạn và nên là một phần của cách tiếp cận bảo mật dữ liệu đa lớp, rộng lớn hơn.
