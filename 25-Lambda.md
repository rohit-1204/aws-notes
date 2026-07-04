# AWS Notes
# Chapter 25 - AWS Lambda

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is AWS Lambda?
2. Why Use Lambda?
3. Serverless Computing
4. How Lambda Works
5. Lambda Components
6. Supported Runtimes
7. Event Sources
8. Execution Flow
9. Lambda Layers
10. Environment Variables
11. Concurrency
12. Monitoring & Logging
13. Lambda Pricing
14. AWS CLI Commands
15. Best Practices
16. Common Use Cases
17. Summary
18. Interview Questions
19. Practice Exercises
20. Mini Project
21. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand AWS Lambda
- Learn Serverless Computing
- Create Lambda Functions
- Trigger Lambda using AWS Services
- Monitor Lambda executions
- Deploy production-ready serverless applications

---

# 📖 What is AWS Lambda?

**AWS Lambda** is a **Serverless Compute Service** that allows you to run code without managing servers.

You simply upload your code, and AWS:

- 🚀 Runs it
- 📈 Scales automatically
- 🔄 Handles availability
- 🖥️ Manages infrastructure

You only pay for the compute time your code uses.

---

# 💡 Why Use Lambda?

Traditional Application:

```text
Application

↓

EC2 Server

↓

Operating System

↓

Infrastructure Management
```

You manage everything.

---

Using Lambda:

```text
Upload Code

↓

AWS Lambda

↓

AWS Manages Servers

↓

Application Executes
```

Benefits:

- ✅ No server management
- ✅ Automatic scaling
- ✅ High availability
- ✅ Pay only for execution time

---

# ☁️ What is Serverless Computing?

**Serverless** does **not** mean there are no servers.

It means:

- AWS manages the servers.
- You focus only on writing code.

Responsibilities:

| You Manage | AWS Manages |
|------------|-------------|
| Code | Servers |
| Business Logic | OS |
| Application | Scaling |
| Function Logic | Infrastructure |

---

# 🧠 How AWS Lambda Works

Execution Flow:

```text
User Request

↓

AWS Service Trigger

↓

Lambda Function

↓

Execute Code

↓

Return Response
```

Example:

```text
Image Uploaded to S3

↓

Lambda Triggered

↓

Resize Image

↓

Save Processed Image
```

---

# 🧩 Lambda Components

A Lambda Function consists of:

- 📝 Function Code
- ⚙️ Runtime
- 🔐 IAM Execution Role
- 🌍 Environment Variables
- 📦 Deployment Package
- 📊 CloudWatch Logs

---

# 💻 Supported Runtimes

AWS Lambda supports multiple programming languages.

| Runtime | Supported |
|----------|-----------|
| Python | ✅ |
| Node.js | ✅ |
| Java | ✅ |
| Go | ✅ |
| .NET | ✅ |
| Ruby | ✅ |
| Custom Runtime | ✅ |

Example:

```python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": "Hello AWS Lambda!"
    }
```

---

# ⚡ Event Sources

Lambda can be triggered by many AWS services.

| AWS Service | Trigger |
|-------------|----------|
| Amazon S3 | File Upload |
| API Gateway | HTTP Request |
| CloudWatch | Scheduled Event |
| DynamoDB | Table Changes |
| SNS | Notifications |
| SQS | Queue Messages |
| EventBridge | Events |
| CloudFront | Edge Requests |

---

# 🔄 Lambda Execution Flow

```text
Event

↓

Lambda Service

↓

Execution Environment

↓

Run Function

↓

Return Output
```

Each execution is isolated and managed by AWS.

---

# 📦 Lambda Layers

**Lambda Layers** allow you to share common libraries across multiple Lambda functions.

Example:

```
Layer

├── Python Packages

├── Shared Libraries

└── Utilities
```

Benefits:

- Reduce deployment size
- Reuse code
- Easier maintenance

---

# 🌍 Environment Variables

Store configuration outside your code.

Example:

```
DB_HOST=database.example.com

DB_PORT=3306

ENV=production
```

Benefits:

- No hardcoded values
- Easy configuration
- Environment-specific settings

---

# 🚀 Concurrency

Lambda automatically scales based on incoming requests.

Example:

```text
100 Requests

↓

100 Lambda Executions
```

Types:

- Default Concurrency
- Reserved Concurrency
- Provisioned Concurrency

Provisioned Concurrency reduces cold starts.

---

# 📊 Monitoring & Logging

Lambda integrates with:

- 📈 Amazon CloudWatch
- 📜 AWS CloudTrail
- 🔍 AWS X-Ray

CloudWatch provides:

- Execution Logs
- Duration
- Errors
- Invocations
- Throttles

---

# 💰 Lambda Pricing

Pricing depends on:

- Number of requests
- Execution duration
- Memory allocated

Formula:

```text
Cost = Requests + Compute Time
```

You only pay when your function runs.

---

# 🏗️ AWS Lambda Architecture

```text
          User / Event
               │
               ▼
      API Gateway / S3 / SNS
               │
               ▼
          AWS Lambda
               │
        ┌──────┴──────┐
        ▼             ▼
 CloudWatch Logs   IAM Role
        │
        ▼
  Other AWS Services
```

---

# 💻 Useful AWS CLI Commands

## List Functions

```bash
aws lambda list-functions
```

---

## Create Function

```bash
aws lambda create-function \
--function-name MyFunction
```

---

## Invoke Function

```bash
aws lambda invoke \
--function-name MyFunction \
response.json
```

---

## Update Function Code

```bash
aws lambda update-function-code \
--function-name MyFunction \
--zip-file fileb://function.zip
```

---

## Delete Function

```bash
aws lambda delete-function \
--function-name MyFunction
```

---

## View Function Configuration

```bash
aws lambda get-function \
--function-name MyFunction
```

---

# 💡 Best Practices

✅ Keep functions small and focused.

✅ Use IAM roles with least privilege.

✅ Store secrets in AWS Secrets Manager.

✅ Use environment variables for configuration.

✅ Monitor functions with CloudWatch.

✅ Reuse libraries using Lambda Layers.

✅ Minimize cold starts.

✅ Set appropriate memory and timeout values.

---

# 🌍 Common Use Cases

| Use Case | Lambda |
|-----------|---------|
| REST APIs | ✅ |
| Image Processing | ✅ |
| File Conversion | ✅ |
| Scheduled Jobs | ✅ |
| Data Processing | ✅ |
| Automation | ✅ |
| Event Processing | ✅ |
| Backend for Mobile Apps | ✅ |

---

# 📝 Key Takeaways

- AWS Lambda is a serverless compute service.
- No server management is required.
- Automatically scales with demand.
- Supports multiple programming languages.
- Integrates with many AWS services.
- Uses CloudWatch for monitoring.
- Pay only for execution time.

---

# 📋 Summary

In this chapter, you learned:

- AWS Lambda
- Serverless Computing
- Lambda Components
- Event Sources
- Execution Flow
- Lambda Layers
- Environment Variables
- Concurrency
- Monitoring
- Pricing
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is AWS Lambda?
2. What is Serverless Computing?
3. Which programming languages are supported?
4. What triggers a Lambda function?
5. How are Lambda functions billed?

---

## Intermediate

6. Explain Lambda Layers.
7. What are environment variables?
8. What is Provisioned Concurrency?
9. How does Lambda integrate with CloudWatch?
10. Explain the Lambda execution lifecycle.

---

## Advanced

11. Design a serverless image-processing application.
12. Compare AWS Lambda and Amazon EC2.
13. Explain cold starts and how to reduce them.
14. How would you secure a Lambda function?
15. Explain how Lambda integrates with API Gateway and EventBridge.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Lambda function using Python.

---

## Exercise 2

Invoke the function using the AWS Console.

---

## Exercise 3

Upload a file to an S3 bucket and trigger Lambda automatically.

---

## Exercise 4

Store a configuration value using environment variables.

---

## Exercise 5

Monitor function execution using CloudWatch Logs.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-lambda-guide.md
```

Include:

- Lambda Overview
- Serverless Computing
- Lambda Components
- Event Sources
- Layers
- Environment Variables
- Monitoring
- Pricing
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add AWS Lambda guide"
```

---

# 📚 Further Reading

- AWS Lambda Documentation
- AWS Lambda Developer Guide
- AWS Serverless Application Model (SAM)
- AWS Lambda Best Practices
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 26 – AWS CloudFormation**, you'll learn:

- ☁️ Infrastructure as Code (IaC)
- 📄 CloudFormation Templates
- 📦 Resources
- 🧩 Parameters
- 📤 Outputs
- 🔄 Stacks & Change Sets
- 🛡️ Stack Policies
- 💻 AWS CLI Commands
- 🚀 Hands-on CloudFormation Labs
