---
title: "Blog 3"
date: "2025-11-25"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


# Dynamic text-to-SQL for enterprise workloads with Amazon Bedrock Agents

Authors: Jiwon Yeom and Jimin Kim | April 14, 2025 | [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Bedrock Agents](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-agents/), [Best Practices](https://aws.amazon.com/blogs/machine-learning/category/post-types/best-practices/), [Generative AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/generative-ai/), [Technical How-to](https://aws.amazon.com/blogs/machine-learning/category/post-types/technical-how-to/), [Thought Leadership](https://aws.amazon.com/blogs/machine-learning/category/post-types/thought-leadership/)  | [Permalink](https://aws.amazon.com/blogs/machine-learning/dynamic-text-to-sql-for-enterprise-workloads-with-amazon-bedrock-agents/) | [Comments](https://aws.amazon.com/blogs/machine-learning/dynamic-text-to-sql-for-enterprise-workloads-with-amazon-bedrock-agents/#Comments) | [Share](https://aws.amazon.com/blogs/machine-learning/dynamic-text-to-sql-for-enterprise-workloads-with-amazon-bedrock-agents/)

[Generative AI](https://aws.amazon.com/generative-ai/) enables us to accomplish more in less time. Text-to-SQL empowers people to explore data and draw insights using natural language, without requiring specialized database knowledge. [Amazon Web Services](https://aws.amazon.com/) (AWS) has helped many customers connect this text-to-SQL capability with their own data, which means more employees can generate insights. In this process, we discovered that a different approach is needed in enterprise environments where there are over 100 tables, each with dozens of columns. We also learned that robust error handling is critical when errors occur in the generated SQL query based on users' questions.

This post demonstrates how enterprises can implement a scalable agentic text-to-SQL solution using [Amazon Bedrock Agents](https://aws.amazon.com/bedrock/agents/), with advanced error-handling tools and automated schema discovery to enhance database query efficiency. Our agent-based solution offers two key strengths:

1. **Automated scalable schema discovery** – The schema and table metadata can be dynamically updated to generate SQL when the initial attempt to execute the query fails. This is important for enterprise customers who have a lot of tables and columns and many queries patterns.
2. **Automated error handling** – The error message is directly fed back to the agent to improve the success rate of running queries.

You'll find that these features help you tackle enterprise-scale database challenges while making your text-to-SQL experience more robust and efficient.

## Use case

An agentic text-to-SQL solution can benefit enterprises with complex data structures. In this post, to understand the mechanics and benefits of the agentic text-to-SQL solution in a complex enterprise environment, imagine you're a business analyst on the risk management team in a bank. You need to answer questions such as "Find all transactions that occurred in the United States and were flagged as fraudulent, along with the device information used for those transactions," or "Retrieve all transactions for John Doe that occurred between January 1, 2023, and December 31, 2023, including fraud flags and merchant details." For this, there are dozens—or sometimes hundreds—of tables that you need to not only be aware but also craft complex JOIN queries. The following diagram illustrates a sample table schema that might be needed for fraud investigations.

![Sample table schema for fraud investigations](/images/3-BlogsTranslated/Blog3/image1.jpg)

The key pain points of implementing a text-to-SQL solution in this complex environment include the following, but aren't limited to:

1. The amount of table information and schema will get excessive, which will entail manual updates on the prompts and limit its scale.
2. As a result, the solution might require additional validation, impacting the quality and performance of generating SQL.

Now, consider our solution and how it addresses these problems.

## Solution overview

Amazon Bedrock Agents seamlessly manages the entire process from question interpretation to query execution and result interpretation, without manual intervention. It seamlessly incorporates multiple tools, and the agent analyzes and responds to unexpected results. When queries fail, the agent autonomously analyzes error messages, modifies queries, and retries—a key benefit over static systems.

As of December 2024, the [Amazon Bedrock with structured data](https://aws.amazon.com/about-aws/whats-new/2024/12/amazon-bedrock-knowledge-bases-structured-data-retrieval/) feature provides built-in support for [Amazon Redshift](https://aws.amazon.com/redshift/), offering seamless text-to-SQL capabilities without custom implementation. This is recommended as the primary solution for Amazon Redshift users.

Here are the capabilities that this solution offers:

### **Executing text-to-SQL with autonomous troubleshooting:**

1. The agent can interpret natural language questions and convert them into SQL queries. It then executes these queries against an [Amazon Athena](https://aws.amazon.com/athena/) database and returns the results.
2. If a query execution fails, the agent can analyze the error messages returned by [AWS Lambda](https://aws.amazon.com/lambda/) and automatically retries the modified query when appropriate.

### **Dynamic schema discovery**

1. Listing tables – The agent can provide a comprehensive list of the tables in the fraud detection database. This helps users understand the available data structures.
2. Describing table schemas – Users can request detailed information about the schema of specific tables. The agent will provide column names, data types, and associated comments, giving users a clear understanding of the data structure.

The solution uses direct database tools for schema discovery instead of vector store–based retrieval or static schema definitions. This approach provides complete accuracy with lower operational overhead because it doesn't require a synchronization mechanism and continually reflects the current database structure. Direct schema access through tools is more maintainable than hardcoded approaches that require manual updates, and it provides better performance and cost-efficiency through real-time database interaction.

The workflow is as follows:

1. A user asks questions to Amazon Bedrock Agents.
2. To serve the user's questions, the agent determines the appropriate action to invoke:
   * To execute the generated query with confidence, the agent will invoke the athena-query
   * To confirm the database schema first, the agent will invoke the athena-schema-reader tool:
      * Retrieve a list of available tables using its /list_tables endpoint.
      * Obtain the specific schema of a certain table using its /describe_table endpoint.
3. The Lambda function sends the query to Athena to execute.
4. Athena queries the data from the [Amazon Simple Storage Service](https://aws.amazon.com/s3/) (Amazon S3) data bucket and stores the query results in the S3 output bucket.
5. The Lambda function retrieves and processes the results. If an error occurs:
   * The Lambda function captures and formats the error message for the agent to understand.
   * The error message is returned to Amazon Bedrock Agents.
6. The agent analyzes the error message and tries to resolve it. To retry with the modified query, the agent may repeat steps 2–5.
7. The agent formats and presents the final responses to the user.

The following architecture diagram shows this workflow.

![Architecture diagram](/images/3-BlogsTranslated/Blog3/image2.png)

## **Implementation walkthrough**

To implement the solution, use the instructions in the following sections.

### **Intelligent error handling**

Our agentic text-to-SQL solution implements practical error handling that helps agents understand and recover from issues. By structuring errors with consistent elements, returning nonbreaking errors where possible, and providing contextual hints, the system enables agents to self-correct and continue their reasoning process.

#### **Agent instructions**

Consider the key prompt components that make this solution unique. Intelligent error handling helps automate troubleshooting and refine the query by letting the agent understand the type of errors and what to do when error happens:

```
Execution and Error Handling:
   - Execute the query via the /athena_query endpoint
   - If the execution fails, carefully analyze the error message and hint provided by the Lambda function
   - Based on the error type received from the Lambda function, take appropriate action:
   - After identifying the issue based on the error message and hint:
     1. Modify your query or API request to address the specific problem
     2. If needed, use schema discovery tools (/list_tables, /describe_table) to gather updated information
     3. Reconstruct the query with the necessary corrections
     4. Retry the execution with the modified query or request
```

The prompt gives guidance on how to approach the errors. It also states that the error types and hints will be provided by Lambda. In the next section, we explain how Lambda processes the errors and passes them to the agent.

#### **Implementation details**

Here are some key examples from our error handling system:

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

These error types cover the main scenarios in text-to-SQL interactions:

1. **Query execution failures** – Handles syntax errors and table reference issues, guiding the agent to use the correct table names and SQL syntax
2. **Result retrieval issues** – Addresses permission problems and invalid column references, helping the agent verify the schema and access rights
3. **API validation** – Verifies that basic requirements are met before query execution, minimizing unnecessary API calls

Each error type includes both an explanatory message and an actionable hint, enabling the agent to take appropriate corrective steps. This implementation shows how straightforward it can be to enable intelligent error handling; instead of handling errors traditionally within Lambda, we return structured error messages that the agent can understand and act upon.

### **Dynamic schema discovery**

The schema discovery is pivotal to keeping Amazon Bedrock Agents consuming the most recent and relevant schema information.

#### **Agent instructions**

Instead of hardcoded database schema information, we allow the agent to discover the database schema dynamically. We've created two API endpoints for this purpose:

```
Schema Discovery:
    - Use /list_tables endpoint to identify available tables in the database
    - Use /describe_table endpoint to get detailed schema information for specific tables
    - Always use the most recent and relevant table schemas, as the database structure may change frequently
    - Before constructing queries, ensure you have up-to-date schema information
```

#### **Implementation details**

Based on the agent instructions, the agent will invoke the appropriate API endpoint.

The /list_tables endpoint lists the tables in a specified database. This is particularly useful when you have multiple databases or frequently add new tables:

```python
@app.post("/list_tables", description="Retrieve a list of all tables in the specified database")
def list_tables(event, database_name):
    query = f"SHOW TABLES IN {database_name}"
    result = execute_and_get_results(query, s3_output)
    if isinstance(result, dict) and 'error' in result:
        return create_api_response(event, 400, get_error_response('QUERY_RESULT_ERROR'))
    return create_api_response(event, 200, result)
```

The /describe_table endpoint reads a specific table's schema with details. We use the "DESCRIBE" command, which includes column comments along with other schema details. These comments help the agent better understand the meaning of the individual columns:

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

When implementing a dynamic schema reader, consider including comprehensive column descriptions to enhance the agent's understanding of the data model.

These endpoints enable the agent to maintain an up-to-date understanding of the database structure, improving its ability to generate accurate queries and adapt to changes in the schema.

## **Demonstration**

You might not experience the exact same response with the presented screenshot due to the indeterministic nature of [large language models](https://aws.amazon.com/what-is/large-language-model/) (LLMs).

The solution is available for you to deploy in your environment with sample data. Clone the repository from [this GitHub link](https://github.com/aws-samples/sample-Dynamic-Text-to-SQL-with-Amazon-Bedrock-Agent) and follow the README guidance. After you deploy the two stacks—AwsText2Sql-DbStack and AwsText2Sql-AgentStack—follow these steps to put the solution in action:

1. Go to [Amazon Bedrock](https://console.aws.amazon.com/bedrock) and select Agents.
2. Select AwsText-to-SQL-AgentStack-DynamicAgent and test by asking questions in the Test window on the right.
3. Example interactions:
   * Which demographic groups or industries are most frequently targeted by fraudsters? Present aggregated data.
   * What specific methods or techniques are commonly used by perpetrators in the reported fraud cases?
   * What patterns or trends can we identify in the timing and location of fraud incidents?
   * Show the details of customers who have made transactions with merchants located in Denver.
   * Provide a list of all merchants along with the total number of transactions they've processed and the number of those transactions that were flagged as fraudulent.
   * List the top five customers based on the highest transaction amounts they've made.

![Testing the agent](/images/3-BlogsTranslated/Blog3/image3.jpg)

4. Choose Show trace and examine each step to understand what tools are used and the agent's rationale for approaching your question, as shown in the following screenshot.

![Show trace](/images/3-BlogsTranslated/Blog3/image4.jpg)

5. (Optional) You can test the Amazon Bedrock Agents [code interpreter](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-code-interpretation.html) by enabling it in Agent settings. Follow the instructions at [Enable code interpretation in Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-enable-code-interpretation.html) and ask the agent "Create a bar chart showing the top three cities that have the most fraud cases."

![Code interpreter example](/images/3-BlogsTranslated/Blog3/image5.jpg)

## **Best practices**

Building on our discussion of dynamic schema discovery and intelligent error handling, here are key practices to optimize your agentic text-to-SQL solution:

1. **Use dynamic schema discovery and error handling** – Use endpoints such as /list_tables and /describe_table to allow the agent to dynamically adapt to your database structure. Implement comprehensive error handling as demonstrated earlier, enabling the agent to interpret and respond to various error types effectively.
2. **Balance static and dynamic information** – Although dynamic discovery is powerful, consider including crucial, stable information in the prompt. This might include database names, key table relationships, or frequently used tables that rarely change. Striking this balance can improve performance without sacrificing flexibility.
3. **Tailoring to your environment** – We designed the sample to always invoke /list_tables and /describe_table, and your implementation might need adjustments. Consider your specific database engine's capabilities and limitations. You might need to provide additional context beyond only column comments. Think about including database descriptions, table relationships, or common query patterns. The key is to give your agent as much relevant information as possible about your data model and business context, whether through extended metadata, custom endpoints, or detailed instructions.
4. **Implement robust data protection** – Although our solution uses Athena, which inherently doesn't support write operations, it's crucial to consider data protection in your specific environment. Start with clear instructions in the prompt (for example, "read-only operations only"), and consider additional layers such as [Amazon Bedrock Guardrails](https://aws.amazon.com/bedrock/guardrails/) or an LLM-based review system to make sure that generated queries align with your security policies.
5. **Implement layered authorization** – To enhance data privacy when using Amazon Bedrock Agents, you can use services such as [Amazon Verified Permissions](https://aws.amazon.com/verified-permissions) to validate user access before the agent processes sensitive data. Pass user identity information, such as a JWT token, to the agent and its associated Lambda function, enabling fine-grained authorization checks against pre-built policies. By enforcing access control at the application level based on the Verified Permissions decision, you can mitigate unintended data disclosure and maintain strong data isolation. To learn more, refer to [Enhancing data privacy with layered authorization for Amazon Bedrock Agents](https://aws.amazon.com/blogs/security/enhancing-data-privacy-with-layered-authorization-for-amazon-bedrock-agents/) in the AWS Security Blog.
6. **Identify the best orchestration strategy for your agent** – Amazon Bedrock provides you with an option to customize your agent's orchestration strategy. [Custom orchestration](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-custom-orchestration.html) gives you full control of how you want your agents to handle multistep tasks, make decisions, and execute workflows.

By implementing these practices, you can create a text-to-SQL solution that not only uses the full potential of AI agents, it also maintains the security and integrity of your data systems.

## **Conclusion**

In conclusion, the implementation of a scalable agentic text-to-SQL solution using AWS services offers significant advantages for enterprise workloads. By using automated schema discovery and robust error handling, organizations can efficiently manage complex databases with numerous tables and columns. The agent-based approach promotes dynamic query generation and refinement, leading to higher success rates in data querying. We'd like to invite you to try this solution out today! Visit [GitHub](https://github.com/aws-samples/sample-Dynamic-Text-to-SQL-with-Amazon-Bedrock-Agent) to dive deeper into the details of the solution, and follow the deployment guide to test in your AWS account.
