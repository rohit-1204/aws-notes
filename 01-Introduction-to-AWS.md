# AWS Notes
# Chapter 01 - Introduction to AWS

> **Level:** Beginner
> **Estimated Reading Time:** 45–60 minutes
> **Practice Time:** 1–2 hours

---

# Table of Contents

1. What is Cloud Computing?
2. What is AWS?
3. Why Learn AWS?
4. Benefits of Cloud Computing
5. Cloud Computing Models
6. Cloud Deployment Models
7. AWS Global Infrastructure
8. AWS Services Overview
9. AWS Free Tier
10. AWS Pricing Model
11. Creating an AWS Account
12. AWS Management Console
13. AWS CLI
14. AWS SDK
15. Shared Responsibility Model
16. AWS Well-Architected Framework
17. AWS Use Cases
18. Summary
19. Interview Questions
20. Practice Exercises
21. Mini Project
22. Further Reading

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand Cloud Computing
- Explain what AWS is
- Understand AWS Global Infrastructure
- Know AWS pricing basics
- Understand the AWS Free Tier
- Navigate the AWS Management Console
- Understand the Shared Responsibility Model
- Prepare your AWS environment for future chapters

---

# What is Cloud Computing?

Cloud Computing is the delivery of computing resources over the Internet instead of owning and maintaining physical hardware.

Instead of purchasing servers, networking devices, and storage, you rent these resources from a cloud provider whenever you need them.

Think of cloud computing like electricity.

Instead of generating electricity at home, you simply consume it and pay only for what you use.

---

# Traditional IT vs Cloud Computing

| Traditional Infrastructure | Cloud Computing |
|---------------------------|----------------|
| Buy physical servers | Rent virtual servers |
| High upfront cost | Pay only for usage |
| Manual scaling | Automatic scaling |
| Weeks to deploy | Minutes to deploy |
| Hardware maintenance required | Managed by cloud provider |
| Limited availability | Global availability |

---

# What is AWS?

AWS (Amazon Web Services) is the world's largest cloud computing platform provided by Amazon.

It offers hundreds of cloud services including:

- Virtual Servers
- Storage
- Databases
- Networking
- Artificial Intelligence
- Machine Learning
- Security
- Monitoring
- Analytics
- Containers

AWS allows individuals and organizations to build applications without managing physical infrastructure.

---

# Why Learn AWS?

AWS is the most widely used cloud platform in the world.

It powers:

- Startups
- Enterprise applications
- Government organizations
- Banks
- E-commerce platforms
- Streaming services
- DevOps pipelines
- Machine Learning applications

Learning AWS is valuable because it is a core skill for:

- Cloud Engineer
- DevOps Engineer
- Site Reliability Engineer (SRE)
- Platform Engineer
- Solutions Architect
- Cloud Administrator

---

# Benefits of AWS

AWS provides many advantages over traditional infrastructure.

## Scalability

Increase or decrease resources based on demand.

## High Availability

Applications can run across multiple data centers.

## Reliability

Services are designed to minimize downtime.

## Global Reach

Deploy applications in multiple countries.

## Security

AWS provides advanced security tools and compliance standards.

## Cost Effective

Pay only for the resources you consume.

---

# Cloud Computing Service Models

Cloud services are commonly divided into three models.

| Model | Description | Examples |
|--------|-------------|----------|
| IaaS | Infrastructure as a Service | Amazon EC2 |
| PaaS | Platform as a Service | AWS Elastic Beanstalk |
| SaaS | Software as a Service | Gmail, Microsoft 365 |

---

# Infrastructure as a Service (IaaS)

You manage:

- Operating System
- Applications
- Runtime
- Data

AWS manages:

- Servers
- Storage
- Networking
- Virtualization

Example:

```
Amazon EC2
```

---

# Platform as a Service (PaaS)

AWS manages:

- Infrastructure
- Operating System
- Runtime

You manage:

- Application
- Data

Example:

```
AWS Elastic Beanstalk
```

---

# Software as a Service (SaaS)

Everything is managed by the provider.

Users simply use the software.

Examples:

- Gmail
- Dropbox
- Microsoft 365

---

# Cloud Deployment Models

## Public Cloud

Infrastructure shared by many customers.

Example:

AWS

---

## Private Cloud

Infrastructure dedicated to a single organization.

---

## Hybrid Cloud

Combination of on-premises infrastructure and cloud resources.

---

# AWS Global Infrastructure

AWS operates data centers around the world.

The infrastructure consists of:

```
AWS Global Infrastructure

        Regions
            │
            ▼
 Availability Zones
            │
            ▼
     Data Centers
```

---

# AWS Region

A Region is a physical geographic location.

Examples:

- US East (N. Virginia)
- Europe (Frankfurt)
- Asia Pacific (Mumbai)

Each region is isolated from other regions.

---

# Availability Zone (AZ)

Each AWS Region contains multiple Availability Zones.

Each Availability Zone consists of one or more data centers.

Benefits:

- Fault tolerance
- High availability
- Disaster recovery

---

# Edge Locations

Edge Locations are used by AWS CloudFront and other services to deliver content closer to users.

Benefits:

- Lower latency
- Faster content delivery

---

# Popular AWS Services

## Compute

- Amazon EC2
- AWS Lambda
- ECS
- EKS

---

## Storage

- Amazon S3
- Amazon EBS
- Amazon EFS

---

## Networking

- Amazon VPC
- Route 53
- Elastic Load Balancer

---

## Database

- Amazon RDS
- DynamoDB

---

## Security

- IAM
- KMS
- Secrets Manager

---

## Monitoring

- CloudWatch
- CloudTrail

---

## DevOps

- CodeCommit
- CodeBuild
- CodeDeploy
- CodePipeline
- CloudFormation

---

# AWS Free Tier

AWS provides a Free Tier for new users.

It allows limited usage of many services for learning purposes.

Examples include:

- EC2
- S3
- Lambda
- DynamoDB
- RDS

Always monitor your usage to avoid unexpected charges.

---

# AWS Pricing Model

AWS generally follows a Pay-As-You-Go pricing model.

Pricing depends on:

- Compute hours
- Storage used
- Data transfer
- API requests

You only pay for what you consume.

---

# Creating an AWS Account

Steps:

1. Visit the AWS website.
2. Create an Amazon account.
3. Verify your email and phone number.
4. Add a payment method.
5. Choose the Free Tier plan.
6. Sign in to the AWS Management Console.

---

# AWS Management Console

The AWS Management Console is a web-based interface used to manage AWS resources.

Using the console, you can:

- Launch EC2 instances
- Create S3 buckets
- Configure IAM users
- Monitor CloudWatch metrics

---

# AWS Command Line Interface (CLI)

The AWS CLI allows you to manage AWS resources from the terminal.

Example:

```bash
aws --version
```

List S3 buckets:

```bash
aws s3 ls
```

The AWS CLI is essential for automation and DevOps workflows.

---

# AWS SDK

AWS provides Software Development Kits (SDKs) for programming languages such as:

- Python (Boto3)
- Java
- JavaScript
- Go
- .NET
- PHP

Developers use SDKs to interact with AWS services programmatically.

---

# Shared Responsibility Model

AWS security is shared between AWS and the customer.

| AWS Responsibility | Customer Responsibility |
|-------------------|-------------------------|
| Physical security | IAM users |
| Hardware | Operating System |
| Networking | Applications |
| Virtualization | Data |
| Managed services | Access management |

Remember:

> **AWS secures the cloud, while you secure what you place in the cloud.**

---

# AWS Well-Architected Framework

AWS recommends building applications using five pillars:

- Operational Excellence
- Security
- Reliability
- Performance Efficiency
- Cost Optimization

These principles help design secure, reliable, and efficient cloud architectures.

---

# Common AWS Use Cases

AWS is commonly used for:

- Website Hosting
- Application Hosting
- CI/CD Pipelines
- Container Platforms
- Kubernetes
- Big Data
- Machine Learning
- Backup & Disaster Recovery
- Media Streaming
- IoT Applications

---

# Key Takeaways

- AWS is the leading cloud platform.
- Cloud computing removes the need to manage physical infrastructure.
- AWS offers services for compute, storage, networking, databases, and security.
- AWS follows a Pay-As-You-Go pricing model.
- Understanding the Shared Responsibility Model is critical.
- AWS skills are essential for DevOps Engineers.

---

# Summary

In this chapter, you learned:

- Cloud Computing fundamentals
- AWS overview
- Benefits of AWS
- Cloud service models
- Deployment models
- AWS Global Infrastructure
- AWS pricing
- AWS Free Tier
- AWS Console
- AWS CLI
- AWS SDK
- Shared Responsibility Model
- Well-Architected Framework

---

# Interview Questions

## Beginner

1. What is Cloud Computing?
2. What is AWS?
3. What are the benefits of AWS?
4. What is the AWS Free Tier?
5. What is a Region?

---

## Intermediate

6. Explain the difference between IaaS, PaaS, and SaaS.
7. What is an Availability Zone?
8. What is the AWS Shared Responsibility Model?
9. What is AWS CLI?
10. What is the purpose of AWS SDKs?

---

## Advanced

11. Why are multiple Availability Zones important?
12. Explain the AWS Well-Architected Framework.
13. How does AWS pricing work?
14. Why is AWS popular among DevOps Engineers?

---

# Practice Exercises

## Exercise 1

Research the AWS services used for:

- Compute
- Storage
- Networking
- Databases

---

## Exercise 2

List three advantages of cloud computing over traditional infrastructure.

---

## Exercise 3

Compare:

- IaaS
- PaaS
- SaaS

in your own words.

---

## Exercise 4

Visit the AWS console (or explore screenshots if you don't have an account) and identify:

- EC2
- S3
- IAM
- CloudWatch

---

## Exercise 5

Draw the AWS Global Infrastructure hierarchy:

```
Region
   │
Availability Zone
   │
Data Center
```

---

# Mini Project

Create a Markdown file named:

```text
aws-overview.md
```

Include:

- What is AWS?
- Benefits of AWS
- Three cloud service models
- AWS Global Infrastructure diagram
- Five popular AWS services
- Three use cases for AWS

Commit it to your Git repository:

```bash
git add .
git commit -m "Add AWS introduction notes"
```

---

# Further Reading

- AWS Global Infrastructure
- AWS Free Tier
- AWS Pricing Calculator
- AWS Well-Architected Framework
- AWS CLI Documentation

---

# What's Next?

In **Chapter 02 – AWS Global Infrastructure**, you'll learn:

- Regions
- Availability Zones
- Local Zones
- Edge Locations
- Data Centers
- Region selection strategies
- High Availability
- Disaster Recovery
- Global application deployment
- Best practices for designing resilient AWS architectures
