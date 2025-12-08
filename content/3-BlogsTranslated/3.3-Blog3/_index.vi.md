---
title: "Blog 3"
date: "2025-11-25"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


# Workload Text-to-SQL linh hoạt cho doanh nghiệp bằng Amazon Bedrock Agent

Tác giả: Jiwon Yeom và Jimin Kim | Ngày 14 Tháng 4, 2025 | [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Bedrock Agents](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-agents/), [Best Practices](https://aws.amazon.com/blogs/machine-learning/category/post-types/best-practices/), [Generative AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/generative-ai/), [Technical How-to](https://aws.amazon.com/blogs/machine-learning/category/post-types/technical-how-to/), [Thought Leadership](https://aws.amazon.com/blogs/machine-learning/category/post-types/thought-leadership/)  | [Permalink](https://aws.amazon.com/blogs/machine-learning/dynamic-text-to-sql-for-enterprise-workloads-with-amazon-bedrock-agents/) | [Comments](https://aws.amazon.com/blogs/machine-learning/dynamic-text-to-sql-for-enterprise-workloads-with-amazon-bedrock-agents/#Comments) | [Share](https://aws.amazon.com/blogs/machine-learning/dynamic-text-to-sql-for-enterprise-workloads-with-amazon-bedrock-agents/)

Trí tuệ nhân tạo tạo sinh ([**Generative AI**](https://aws.amazon.com/generative-ai/)) cho phép chúng ta hoàn thành nhiều việc hơn trong thời gian ngắn hơn. Công nghệ **Text-to-SQL** (Chuyển văn bản thành câu lệnh SQL) trao quyền cho mọi người khám phá dữ liệu và rút ra thông tin chi tiết bằng ngôn ngữ tự nhiên, mà không cần kiến thức chuyên sâu về cơ sở dữ liệu. [Amazon Web Services](https://aws.amazon.com/) **(AWS)** đã giúp nhiều khách hàng kết nối khả năng Text-to-SQL này với dữ liệu riêng của họ, nghĩa là sẽ có nhiều nhân viên hơn có thể tạo ra các thông tin chuyên sâu.

Trong quá trình này, chúng tôi nhận thấy cần có một cách tiếp cận khác trong các môi trường doanh nghiệp có hơn 100 bảng, mỗi bảng có hàng chục cột. Chúng tôi cũng nhận thấy rằng, việc xử lý lỗi mạnh mẽ là cực kỳ quan trọng khi xảy ra lỗi trong truy vấn SQL được tạo ra dựa trên câu hỏi của người dùng.

Bài viết này trình bày cách các doanh nghiệp có thể triển khai một giải pháp Text-to-SQL dạng agentic có khả năng mở rộng bằng cách sử dụng [**Amazon Bedrock Agents**](https://aws.amazon.com/bedrock/agents/), với các công cụ xử lý lỗi nâng cao và tính năng khám phá sơ đồ dữ liệu tự động để tăng cường hiệu quả truy vấn cơ sở dữ liệu.

Giải pháp dựa trên agent của chúng tôi mang lại hai thế mạnh chính:

1. **Khám phá sơ đồ dữ liệu tự động có khả năng mở rộng** – Sơ đồ và siêu dữ liệu bảng có thể được cập nhật động để tạo lại câu lệnh SQL khi lần thực thi truy vấn ban đầu thất bại. Điều này rất quan trọng đối với các khách hàng doanh nghiệp có nhiều bảng, nhiều cột và nhiều mẫu truy vấn.  
2. **Xử lý lỗi tự động**  – Thông báo lỗi được đưa trực tiếp trở lại agent (agent) để cải thiện tỷ lệ thành công khi chạy các truy vấn.

Bạn sẽ thấy rằng những tính năng này giúp bạn giải quyết các thách thức về cơ sở dữ liệu quy mô doanh nghiệp, đồng thời làm cho trải nghiệm Text-to-SQL của bạn trở nên mạnh mẽ và hiệu quả hơn.

## **Use Case**

Một giải pháp Text-to-SQL dạng agentic có thể mang lại lợi ích cho các doanh nghiệp có cấu trúc dữ liệu phức tạp. Trong bài đăng này, để hiểu rõ cơ chế và lợi ích của giải pháp Text-to-SQL dạng agentic trong môi trường doanh nghiệp phức tạp, hãy tưởng tượng bạn là một chuyên viên phân tích nghiệp vụ thuộc đội quản lý rủi ro tại một ngân hàng.

Bạn cần trả lời các câu hỏi như: "Tìm tất cả các giao dịch xảy ra ở Hoa Kỳ và bị đánh dấu là gian lận, cùng với thông tin thiết bị được sử dụng cho các giao dịch đó," hoặc "Truy xuất tất cả giao dịch của John Doe xảy ra từ ngày 1 tháng 1 năm 2023 đến ngày 31 tháng 12 năm 2023, bao gồm cả dấu hiệu gian lận và chi tiết về người bán."

Để làm được điều này, bạn cần phải nhận biết và xử lý hàng chục—hoặc đôi khi hàng trăm—bảng, đồng thời phải tạo ra các truy vấn **JOIN phức tạp**. Sơ đồ sau minh họa một sơ đồ bảng mẫu có thể cần thiết cho các cuộc điều tra về việc gian lận.

![Sơ đồ cơ sở dữ liệu mẫu cho phát hiện gian lận](/images/3-BlogsTranslated/Blog3/image1.png)

Những điều khó khăn chính khi triển khai giải pháp Text-to-SQL trong môi trường phức tạp này bao gồm, nhưng không giới hạn ở:

1. Số lượng thông tin bảng và sơ đồ dữ liệu sẽ trở nên quá lớn, điều này đòi hỏi phải cập nhật thủ công các câu lệnh (prompts) và làm hạn chế khả năng mở rộng của giải pháp.  
2. Do đó, giải pháp có thể cần phải xác thực bổ sung, làm ảnh hưởng đến chất lượng và hiệu suất của việc tạo câu lệnh SQL.

## **Tổng quan về Giải pháp**

Amazon Bedrock Agents quản lý toàn bộ quá trình một cách liền mạch, từ việc diễn giải câu hỏi đến thực thi truy vấn và giải thích kết quả, mà không cần can thiệp thủ công. Nó tích hợp nhiều công cụ một cách liền mạch, và agent sẽ phân tích và phản hồi các kết quả không mong muốn. Khi các truy vấn thất bại, agent sẽ tự động phân tích thông báo lỗi, sửa đổi truy vấn và thử lại – đây là một lợi ích then chốt so với các hệ thống tĩnh.

Kể từ tháng 12 năm 2024, tính năng [Amazon Bedrock](https://aws.amazon.com/about-aws/whats-new/2024/12/amazon-bedrock-knowledge-bases-structured-data-retrieval/) với dữ liệu có cấu trúc cung cấp hỗ trợ tích hợp cho Amazon Redshift, mang lại khả năng Text-to-SQL liền mạch mà không cần triển khai tùy chỉnh. Đây được khuyến nghị là giải pháp chính cho người dùng [Amazon Redshift](https://aws.amazon.com/redshift/).

Dưới đây là các khả năng mà giải pháp này mang lại:

### **Thực thi Text-to-SQL với Khả năng Tự động Khắc phục Sự cố:**

1. Agent có thể diễn giải các câu hỏi bằng ngôn ngữ tự nhiên và chuyển chúng thành các truy vấn SQL. Sau đó, nó thực thi các truy vấn này đối với cơ sở dữ liệu [Amazon Athena](https://aws.amazon.com/athena/) và trả về kết quả.  
2. Nếu việc thực thi truy vấn thất bại, agent có thể phân tích các thông báo lỗi được trả về bởi [AWS Lambda](https://aws.amazon.com/lambda/) và tự động thử lại truy vấn đã được sửa đổi khi thích hợp.

### **Khám phá Sơ đồ Dữ liệu Động:** 

1. Liệt kê các bảng: Agent có thể cung cấp danh sách đầy đủ các bảng trong cơ sở dữ liệu phát hiện gian lận. Điều này giúp người dùng hiểu rõ các cấu trúc dữ liệu có sẵn.  
2. Mô tả sơ đồ bảng: Người dùng có thể yêu cầu thông tin chi tiết về sơ đồ của các bảng cụ thể. Agent sẽ cung cấp tên cột, kiểu dữ liệu và các bình luận liên quan, giúp người dùng hiểu rõ cấu trúc dữ liệu.

Giải pháp này sử dụng các công cụ cơ sở dữ liệu trực tiếp để khám phá sơ đồ thay vì truy xuất dựa trên kho vector hoặc các định nghĩa sơ đồ tĩnh. Cách tiếp cận này cung cấp độ chính xác hoàn toàn với chi phí vận hành thấp hơn vì nó không yêu cầu cơ chế đồng bộ hóa và phản ánh liên tục cấu trúc cơ sở dữ liệu hiện tại. Truy cập trực tiếp sơ đồ thông qua các công cụ dễ bảo trì hơn so với các phương pháp mã hóa cứng (hardcoded) đòi hỏi cập nhật thủ công, và nó mang lại hiệu suất và hiệu quả chi phí tốt hơn thông qua tương tác cơ sở dữ liệu theo thời gian thực.

Workflow diễn ra như sau:

1. Người dùng đặt câu hỏi cho **Amazon Bedrock Agents**.  
2. Để phục vụ câu hỏi của người dùng, agent xác định hành động thích hợp để gọi:  
   * Để thực thi truy vấn đã tạo một cách tự tin, agent sẽ gọi công cụ **athena-query**.  
   * Để xác nhận sơ đồ cơ sở dữ liệu trước, agent sẽ gọi công cụ **athena-schema-reader**:  
     * Truy xuất danh sách các bảng có sẵn bằng điểm cuối `/list_tables` của nó.  
     * Lấy sơ đồ cụ thể của một bảng nhất định bằng điểm cuối `/describe_table` của nó.  
3. **Lambda** gửi truy vấn đến **Athena** để thực thi.  
4. **Athena** truy vấn dữ liệu từ **bucket dữ liệu [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/)** và lưu trữ kết quả truy vấn trong bucket đầu ra của S3.  
5. **Lambda** truy xuất và xử lý kết quả. Nếu xảy ra lỗi:  
   * Lambda bắt và định dạng thông báo lỗi để agent hiểu được.  
   * Thông báo lỗi được trả về cho **Amazon Bedrock Agents**.  
6. Agent phân tích thông báo lỗi và cố gắng giải quyết. Để thử lại với truy vấn đã sửa đổi, agent có thể lặp lại các bước 2–5.  
7. Agent định dạng và trình bày phản hồi cuối cùng cho người dùng.

Sơ đồ kiến trúc sau đây cho thấy workflow này:

![Sơ đồ kiến trúc giải pháp](/images/3-BlogsTranslated/Blog3/image2.png)

## **Hướng dẫn Triển khai**

Để triển khai giải pháp, hãy sử dụng các hướng dẫn trong các phần sau.

### **Xử lý Lỗi Thông minh** 

Giải pháp Text-to-SQL dạng agentic của chúng tôi triển khai tính năng xử lý lỗi thực tế giúp các agent hiểu và phục hồi sau các sự cố. Bằng cách cấu trúc hóa các lỗi với các yếu tố nhất quán, trả về các lỗi không gây gián đoạn nếu có thể, và cung cấp các gợi ý theo ngữ cảnh, hệ thống cho phép các agent tự điều chỉnh và tiếp tục quá trình suy luận của chúng.

### **Agent Instructions**

Hãy xem xét các thành phần câu lệnh (prompt components) chính làm cho giải pháp này trở nên độc đáo. Xử lý lỗi thông minh giúp tự động hóa việc khắc phục sự cố và tinh chỉnh truy vấn bằng cách cho agent hiểu loại lỗi và cần làm gì khi lỗi xảy ra:

**Execution and Error Handling:**

- Execute the query via the /athena_query endpoint
- If the execution fails, carefully analyze the error message and hint provided by the Lambda function
- Based on the error type received from the Lambda function, take appropriate action:
- After identifying the issue based on the error message and hint:
  1. Modify your query or API request to address the specific problem
  2. If needed, use schema discovery tools (/list_tables, /describe_table) to gather updated information
  3. Reconstruct the query with the necessary corrections
  4. Retry the execution with the modified query or request

Câu lệnh (prompt) đưa ra hướng dẫn về cách tiếp cận các lỗi. Nó cũng nêu rõ rằng các loại lỗi và gợi ý sẽ được cung cấp bởi Lambda. Trong phần tiếp theo, chúng tôi sẽ giải thích cách Lambda xử lý các lỗi và truyền chúng cho agent.

## **Chi tiết Triển khai**

Dưới đây là một số ví dụ chính từ hệ thống xử lý lỗi của chúng tôi:

```python
ERROR_MESSAGES = {
    'QUERY_EXECUTION_FAILED': {
        'message': 'Failed to execute query',
        'hint': 'Please use fully qualified table names. Example: SELECT * FROM fraud_data.customers LIMIT 1'
    },
    'QUERY_RESULT_ERROR': {
        'message': 'Error occurred while getting query results',
        'hint': 'Check if the tables and columns in your query exist and you have proper permissions. Examples: "customers", "transactions", or "devices".'
    },
    'MISSING_QUERY': {
        'message': 'Query is required',
        'hint': 'No query was provided. Please provide a SQL query to execute'
    }
}

def create_query_response(query_result, status_code=200):
    if query_result.get('error'):
        error_info = ERROR_MESSAGES.get(query_result['error'])
        return {
            'error': query_result['error'],
            'message': error_info['message'],
            'hint': error_info['hint']
        }
    return query_result
```

Các loại lỗi này bao quát các tình huống chính trong tương tác Text-to-SQL:

1. **Lỗi thực thi truy vấn:** Xử lý lỗi cú pháp và các vấn đề về tham chiếu bảng, hướng dẫn agent sử dụng đúng tên bảng và cú pháp SQL.  
2. **Vấn đề truy xuất kết quả:** Giải quyết các vấn đề về quyền hạn và tham chiếu cột không hợp lệ, giúp agent xác minh sơ đồ và quyền truy cập.  
3. **Xác thực API:** Xác minh rằng các yêu cầu cơ bản được đáp ứng trước khi thực thi truy vấn, giảm thiểu các lệnh gọi API không cần thiết.

Mỗi loại lỗi đều bao gồm cả thông báo giải thích và gợi ý hành động, cho phép agent thực hiện các bước điều chỉnh phù hợp. Việc triển khai này cho thấy việc kích hoạt xử lý lỗi thông minh có thể đơn giản như thế nào; thay vì xử lý lỗi theo cách truyền thống trong Lambda, chúng tôi trả về các thông báo lỗi có cấu trúc mà agent có thể hiểu và hành động theo.

## **Khám phá Sơ đồ Dữ liệu Động** 

Khám phá sơ đồ dữ liệu là cột mốc để giữ cho Amazon Bedrock Agents tiếp nhận được thông tin sơ đồ mới nhất và phù hợp nhất.

### **Hướng dẫn cho agent** 

Thay vì thông tin sơ đồ cơ sở dữ liệu được hardcoded, chúng tôi cho phép agent khám phá sơ đồ cơ sở dữ liệu một cách động. Chúng tôi đã tạo ra hai API endpoints cho mục đích này:

**Schema Discovery:**

- Use /list_tables endpoint to identify available tables in the database 
- Use /describe_table endpoint to get detailed schema information for specific tables 
- Always use the most recent and relevant table schemas, as the database structure may change frequently 
- Before constructing queries, ensure you have up-to-date schema information

## **Chi tiết Triển khai**

Dựa trên hướng dẫn của agent, agent sẽ gọi API endpoint thích hợp.

Endpoint `/list_tables` liệt kê các bảng trong một cơ sở dữ liệu được chỉ định. Điều này đặc biệt hữu ích khi bạn có nhiều cơ sở dữ liệu hoặc thường xuyên thêm các bảng mới:

```python
@app.post("/list_tables", description="Retrieve a list of all tables in the specified database")
def list_tables(event, database_name):
    query = f"SHOW TABLES IN {database_name}"
    result = execute_and_get_results(query, s3_output)
    if isinstance(result, dict) and 'error' in result:
        return create_api_response(event, 400, get_error_response('QUERY_RESULT_ERROR'))
    return create_api_response(event, 200, result)
```

Endpoint `/describe_table` đọc sơ đồ của một bảng cụ thể kèm theo các chi tiết. Chúng tôi sử dụng lệnh "DESCRIBE", bao gồm các ghi chú cột (column comments) cùng với các chi tiết sơ đồ khác. Những ghi chú này giúp agent hiểu rõ hơn về ý nghĩa của từng cột:

```python
@app.post("/describe_table", description="Retrieve the schema information of a specific table")
def describe_table(event, database_name, table_name):
    query = f"DESCRIBE {database_name}.{table_name}"
    result = execute_and_get_results(query, s3_output)
    
    if isinstance(result, dict) and 'error' in result:
        return create_api_response(event, 400, get_error_response('QUERY_RESULT_ERROR'))
    
    formatted_result = {
        "table_name": table_name,
        "database": database_name,
        "columns": result
    }
    return create_api_response(event, 200, formatted_result)
```

Khi triển khai bộ đọc sơ đồ dữ liệu động, hãy cân nhắc bao gồm các mô tả cột toàn diện để tăng cường khả năng hiểu của agent về mô hình dữ liệu.

Các API Endpoints này cho phép agent duy trì sự hiểu biết cập nhật về cấu trúc cơ sở dữ liệu, từ đó cải thiện khả năng tạo ra các truy vấn chính xác và thích ứng với những thay đổi trong sơ đồ.

## **Demonstration**

Bạn có thể không nhận được phản hồi chính xác như trong ảnh chụp màn hình được trình bày do tính chất không xác định của các [mô hình ngôn ngữ lớn](https://aws.amazon.com/what-is/large-language-model/) (LLMs).

Giải pháp này đã có sẵn để bạn triển khai trong môi trường của mình với dữ liệu mẫu. Hãy clone kho lưu trữ từ [liên kết GitHub này](https://github.com/aws-samples/sample-Dynamic-Text-to-SQL-with-Amazon-Bedrock-Agent) và làm theo hướng dẫn trong tệp README.

Sau khi bạn triển khai hai stack (**AwsText2Sql-DbStack** và **AwsText2Sql-AgentStack),** hãy làm theo các bước sau để đưa giải pháp vào hoạt động:

1. Truy cập [Amazon Bedrock](https://console.aws.amazon.com/bedrock) và chọn Agents.  
2. Chọn AwsText-to-SQL-AgentStack-DynamicAgent và kiểm tra bằng cách đặt câu hỏi trong cửa sổ Test ở bên phải.  
3. Ví dụ về các tương tác:  
   * Những nhóm nhân khẩu học hoặc ngành công nghiệp nào thường xuyên bị những kẻ gian lận nhắm đến nhất? Trình bày dữ liệu tổng hợp.  
   * Những phương pháp hoặc kỹ thuật cụ thể nào thường được những kẻ phạm tội sử dụng trong các trường hợp gian lận đã được báo cáo?  
   * Chúng ta có thể xác định được những mô hình hoặc xu hướng nào về thời gian và địa điểm xảy ra các sự cố gian lận?  
   * Cho xem chi tiết của những khách hàng đã thực hiện giao dịch với các merchants nằm ở Denver.  
   * Cung cấp một danh sách tất cả các người bán cùng với tổng số giao dịch họ đã xử lý và số lượng các giao dịch đó đã bị đánh dấu là gian lận.  
   * Liệt kê năm khách hàng hàng đầu dựa trên số lượng giao dịch có giá trị cao nhất mà họ đã thực hiện.

![Giao diện test Amazon Bedrock Agent](/images/3-BlogsTranslated/Blog3/image3.png)

4. Hãy chọn "Show trace" (Hiển thị dấu vết) và kiểm tra từng bước để hiểu những công cụ nào được sử dụng và lý do của agent (agent) khi tiếp cận câu hỏi của bạn, như được minh họa trong ảnh chụp màn hình sau.

![Hiển thị trace của agent](/images/3-BlogsTranslated/Blog3/image4.png)

5. (Tùy chọn) Bạn có thể kiểm tra [trình thông dịch mã](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-code-interpretation.html) của Amazon Bedrock Agents bằng cách bật tính năng này trong Cài đặt agent (Agent settings).

Hãy làm theo hướng dẫn tại [Enable code interpretation in Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-enable-code-interpretation.html) và hỏi agent: "Tạo biểu đồ cột thể hiện ba thành phố hàng đầu có số vụ gian lận nhiều nhất."

![Kết quả code interpretation với biểu đồ](/images/3-BlogsTranslated/Blog3/image5.png)

## **Các ví dụ thực tiễn**

Dựa trên cuộc thảo luận của chúng ta về khám phá sơ đồ dữ liệu động và xử lý lỗi thông minh, dưới đây là các thực tiễn chính để tối ưu hóa giải pháp Text-to-SQL dạng agent của bạn:

1. **Sử dụng Khám phá Sơ đồ Dữ liệu và Xử lý Lỗi Động:** Sử dụng các điểm cuối như /list_tables và /describe_table để cho phép agent thích ứng linh hoạt với cấu trúc cơ sở dữ liệu của bạn. Triển khai tính năng xử lý lỗi toàn diện như đã trình bày trước đó, giúp agent diễn giải và phản hồi các loại lỗi khác nhau một cách hiệu quả.  

2. **Cân bằng Thông tin Tĩnh và Động:** Mặc dù khám phá động rất mạnh mẽ, hãy cân nhắc đưa các thông tin quan trọng, ổn định vào câu lệnh (prompt). Điều này có thể bao gồm tên cơ sở dữ liệu, các khoá quan hệ bảng, hoặc các bảng thường xuyên được sử dụng mà ít khi thay đổi. Đạt được sự cân bằng này có thể cải thiện hiệu suất mà không làm mất đi tính linh hoạt.  

3. **Điều chỉnh cho phù hợp với Môi trường của bạn:** Chúng tôi đã thiết kế ví dụ mẫu để luôn gọi /list_tables và /describe_table, nhưng việc triển khai của bạn có thể cần điều chỉnh. Hãy xem xét các khả năng và giới hạn của công cụ cơ sở dữ liệu cụ thể mà bạn sử dụng. Bạn có thể cần cung cấp thêm ngữ cảnh ngoài các ghi chú cột. Hãy cân nhắc bao gồm mô tả cơ sở dữ liệu, mối quan hệ giữa các bảng, hoặc các mẫu truy vấn phổ biến. Điều cốt yếu là cung cấp cho agent càng nhiều thông tin liên quan càng tốt về mô hình dữ liệu và ngữ cảnh kinh doanh của bạn, dù bằng siêu dữ liệu mở rộng, các điểm cuối tùy chỉnh hay hướng dẫn chi tiết.  

4. **Triển khai Bảo vệ Dữ liệu Mạnh mẽ:** Mặc dù giải pháp của chúng tôi sử dụng Athena (vốn không hỗ trợ các thao tác ghi), điều quan trọng là phải xem xét bảo vệ dữ liệu trong môi trường cụ thể của bạn. Bắt đầu với các hướng dẫn rõ ràng trong lời nhắc (ví dụ: "chỉ các thao tác chỉ đọc"), và cân nhắc các lớp bổ sung như [Amazon Bedrock Guardrails](https://aws.amazon.com/bedrock/guardrails/) hoặc hệ thống đánh giá dựa trên LLM để đảm bảo các truy vấn được tạo ra tuân thủ các chính sách bảo mật của bạn.  

5. **Triển khai Ủy quyền Phân lớp:** Để tăng cường quyền riêng tư dữ liệu khi sử dụng Amazon Bedrock Agents, bạn có thể sử dụng các dịch vụ như Amazon Verified Permissions để xác thực quyền truy cập của người dùng trước khi agent xử lý dữ liệu nhạy cảm. Truyền thông tin danh tính người dùng, chẳng hạn như mã thông báo JWT, đến agent và hàm Lambda liên quan của nó, cho phép kiểm tra ủy quyền chi tiết dựa trên các chính sách được xây dựng sẵn. Bằng cách thực thi kiểm soát truy cập ở cấp độ ứng dụng dựa trên quyết định của [Amazon Verified Permissions](https://aws.amazon.com/verified-permissions), bạn có thể giảm thiểu việc tiết lộ dữ liệu ngoài ý muốn và duy trì sự cô lập dữ liệu mạnh mẽ. Để tìm hiểu thêm, hãy tham khảo bài viết "[Enhancing data privacy with layered authorization for Amazon Bedrock Agents](https://aws.amazon.com/blogs/security/enhancing-data-privacy-with-layered-authorization-for-amazon-bedrock-agents/)" trên AWS Security Blog.  

6. **Xác định Chiến lược Điều phối Tốt nhất cho agent của bạn:** Amazon Bedrock cung cấp cho bạn tùy chọn tùy chỉnh chiến lược điều phối của agent. [Điều phối tùy chỉnh](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-custom-orchestration.html) cho phép bạn toàn quyền kiểm soát cách bạn muốn agent xử lý các tác vụ nhiều bước, đưa ra quyết định và thực thi quy trình làm việc.

Bằng cách thực hiện các thực tiễn này, bạn có thể tạo ra một giải pháp Text-to-SQL không chỉ sử dụng toàn bộ tiềm năng của các agent AI mà còn duy trì tính bảo mật và tính toàn vẹn của các hệ thống dữ liệu của bạn.

## **Kết luận**

Tóm lại, việc triển khai một giải pháp Text-to-SQL dạng agent (agentic text-to-SQL) có khả năng mở rộng bằng cách sử dụng các dịch vụ của AWS mang lại những lợi thế đáng kể cho khối lượng công việc cấp doanh nghiệp.

Bằng cách sử dụng tính năng khám phá sơ đồ dữ liệu tự động và xử lý lỗi mạnh mẽ, các tổ chức có thể quản lý hiệu quả các cơ sở dữ liệu phức tạp với vô số bảng và cột. Cách tiếp cận dựa trên agent này thúc đẩy việc tạo và tinh chỉnh truy vấn một cách động, dẫn đến tỷ lệ thành công cao hơn trong việc truy vấn dữ liệu.

Chúng tôi muốn mời bạn trải nghiệm giải pháp này ngay hôm nay! Hãy truy cập [**GitHub**](https://github.com/aws-samples/sample-Dynamic-Text-to-SQL-with-Amazon-Bedrock-Agent) để tìm hiểu sâu hơn về chi tiết giải pháp và làm theo hướng dẫn triển khai để kiểm tra trong tài khoản AWS của bạn.
