# AWS Notes
# Chapter 39 - AWS Interview Questions

> 📘 **Level:** Beginner to Advanced
> ⏱️ **Estimated Reading Time:** 90–120 minutes
> 🛠️ **Practice Time:** 5–6 hours

---

# 📚 Table of Contents

1. Introduction
2. Beginner Questions
3. Intermediate Questions
4. Advanced Questions
5. Scenario-Based Questions
6. Architecture Questions
7. DevOps Questions
8. Security Questions
9. Monitoring Questions
10. Cost Optimization Questions
11. Rapid Fire Questions
12. Interview Tips
13. Summary

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Revise important AWS concepts
- Prepare for AWS interviews
- Answer architecture and DevOps questions
- Understand real-world scenarios
- Improve interview confidence

---

# 📖 Introduction

AWS interviews usually focus on:

- AWS Core Services
- Networking
- Security
- DevOps
- CI/CD
- Containers
- Monitoring
- High Availability
- Cost Optimization
- Real-world architecture design

---

# 🟢 Beginner Questions

### 1. What is AWS?

A cloud computing platform that provides on-demand infrastructure and services.

---

### 2. What is an AWS Region?

A geographical location containing multiple Availability Zones.

---

### 3. What is an Availability Zone (AZ)?

An isolated data center within a Region.

---

### 4. What is Amazon EC2?

A virtual machine service for running applications.

---

### 5. What is Amazon S3?

Object storage service for storing files and backups.

---

### 6. What is Amazon VPC?

A private virtual network in AWS.

---

### 7. What is an Internet Gateway?

Allows communication between a VPC and the internet.

---

### 8. What is a NAT Gateway?

Allows private instances to access the internet without exposing them publicly.

---

### 9. What is an EBS Volume?

Persistent block storage attached to EC2 instances.

---

### 10. What is IAM?

Identity and Access Management service used to manage users, roles, and permissions.

---

# 🟡 Intermediate Questions

### 11. Difference between Security Group and NACL?

| Security Group | Network ACL |
|---------------|-------------|
| Instance Level | Subnet Level |
| Stateful | Stateless |
| Allow Rules Only | Allow & Deny Rules |

---

### 12. Difference between EBS, EFS and S3?

| Service | Storage Type |
|----------|--------------|
| EBS | Block Storage |
| EFS | File Storage |
| S3 | Object Storage |

---

### 13. What is Auto Scaling?

Automatically increases or decreases EC2 instances based on demand.

---

### 14. What is an Elastic Load Balancer?

Distributes incoming traffic across multiple servers.

---

### 15. Difference between ALB and NLB?

| ALB | NLB |
|------|-----|
| HTTP/HTTPS | TCP/UDP |
| Layer 7 | Layer 4 |

---

### 16. What is Route 53?

AWS DNS service for routing internet traffic.

---

### 17. What is CloudWatch?

Monitoring and alerting service.

---

### 18. What is CloudTrail?

Records AWS API activities for auditing.

---

### 19. What is AWS Lambda?

Serverless compute service that runs code without managing servers.

---

### 20. What is CloudFormation?

Infrastructure as Code (IaC) service for provisioning AWS resources using templates.

---

# 🔴 Advanced Questions

### 21. Explain the AWS Shared Responsibility Model.

AWS secures the cloud infrastructure, while customers secure their applications, operating systems, data, and configurations.

---

### 22. Explain High Availability.

Deploy applications across multiple Availability Zones with Load Balancers and Auto Scaling.

---

### 23. Explain Fault Tolerance.

Applications continue working even if one component fails.

---

### 24. What is Disaster Recovery?

A strategy to recover applications and data after failures using backups, Multi-AZ, or Multi-Region deployments.

---

### 25. Difference between Multi-AZ and Multi-Region?

| Multi-AZ | Multi-Region |
|-----------|--------------|
| Same Region | Different Regions |
| High Availability | Disaster Recovery |

---

### 26. Explain AWS KMS.

Service for managing encryption keys used to protect AWS resources and sensitive data.

---

### 27. What is AWS Secrets Manager?

Stores and manages sensitive information such as passwords and API keys.

---

### 28. Difference between ECS and EKS?

| ECS | EKS |
|-----|-----|
| AWS Container Service | Managed Kubernetes |
| Easier Setup | More Flexible |

---

### 29. What is Terraform?

Infrastructure as Code tool used to automate cloud infrastructure provisioning.

---

### 30. Explain Infrastructure as Code (IaC).

Managing infrastructure using configuration files instead of manual creation.

---

# 🌐 Scenario-Based Questions

### 31. A website receives sudden traffic. What AWS services would you use?

- Auto Scaling
- Application Load Balancer
- CloudWatch
- Multi-AZ EC2

---

### 32. How would you secure an S3 bucket?

- Block Public Access
- IAM Policies
- Bucket Policies
- KMS Encryption
- Versioning

---

### 33. How would you deploy a Docker application?

- Build Docker Image
- Push to Amazon ECR
- Deploy using ECS or EKS
- Configure Load Balancer

---

### 34. How would you reduce AWS costs?

- Right-size resources
- Auto Scaling
- Spot Instances
- Savings Plans
- Delete unused resources

---

### 35. How would you troubleshoot a failed EC2 instance?

- Check Instance Status
- Review Security Groups
- Verify Route Tables
- Check CloudWatch Logs
- Review System Logs

---

# 🏗️ Architecture Questions

### 36. Design a highly available web application.

Expected services:

- Route 53
- ALB
- Auto Scaling
- EC2
- RDS Multi-AZ
- CloudWatch
- CloudTrail

---

### 37. Design a secure VPC.

Include:

- Public Subnets
- Private Subnets
- NAT Gateway
- Security Groups
- NACLs
- IAM Roles

---

### 38. Design a CI/CD pipeline.

Pipeline:

```text
Developer

↓

CodeCommit

↓

CodeBuild

↓

CodeDeploy

↓

CodePipeline

↓

Production
```

---

# 🚀 DevOps Questions

### 39. What is CI/CD?

Continuous Integration and Continuous Deployment automate software delivery.

---

### 40. Difference between Docker and Kubernetes?

| Docker | Kubernetes |
|---------|------------|
| Container Platform | Container Orchestration |

---

### 41. Why use Amazon ECR?

Stores Docker images securely.

---

### 42. Difference between ECS and Lambda?

| ECS | Lambda |
|-----|--------|
| Long-running Containers | Event-driven Functions |

---

### 43. Why use CloudFormation or Terraform?

To automate infrastructure deployment using Infrastructure as Code.

---

# 🔐 Security Questions

### 44. Why should MFA be enabled?

Provides an additional authentication factor.

---

### 45. What is the Principle of Least Privilege?

Grant only the permissions required to perform a task.

---

### 46. Why avoid using the Root User?

The root account has unrestricted access and should only be used for account-level tasks.

---

### 47. Difference between IAM Role and IAM User?

| IAM User | IAM Role |
|----------|----------|
| Permanent Identity | Temporary Identity |

---

### 48. What is AWS GuardDuty?

Threat detection service that continuously monitors AWS accounts.

---

# 📊 Monitoring Questions

### 49. Difference between CloudWatch and CloudTrail?

| CloudWatch | CloudTrail |
|------------|------------|
| Metrics & Logs | API Activity |

---

### 50. What is an SNS Notification?

A notification service used to send alerts through email, SMS, or other endpoints.

---

# 💰 Cost Optimization Questions

### 51. Difference between Reserved Instances and Spot Instances?

| Reserved | Spot |
|----------|------|
| Predictable Workloads | Interruptible Workloads |

---

### 52. What is AWS Cost Explorer?

Tool for analyzing AWS spending.

---

### 53. What is AWS Budgets?

Creates spending limits and sends alerts when thresholds are reached.

---

# ⚡ Rapid Fire Questions

- What is VPC?
- What is Route 53?
- What is EBS?
- What is EFS?
- What is S3?
- What is IAM?
- What is KMS?
- What is Lambda?
- What is ECS?
- What is EKS?
- What is CloudWatch?
- What is CloudTrail?
- What is Auto Scaling?
- What is ALB?
- What is Terraform?

---

# 💼 Interview Tips

- ✅ Learn AWS core services thoroughly
- ✅ Practice designing architectures
- ✅ Understand networking basics
- ✅ Know IAM and security concepts
- ✅ Learn Docker, ECS, and EKS
- ✅ Practice Terraform and CloudFormation
- ✅ Understand monitoring and logging
- ✅ Revise cost optimization strategies
- ✅ Build hands-on AWS projects
- ✅ Explain concepts with real-world examples

---

# 📝 Key Takeaways

- AWS interviews cover services, architecture, security, and DevOps.
- Practical experience is as important as theoretical knowledge.
- Focus on explaining *why* a service is used.
- Practice scenario-based questions regularly.
- Build projects to strengthen your understanding.

---

# 📋 Summary

In this chapter, you revised:

- AWS Fundamentals
- Compute Services
- Storage Services
- Networking
- IAM & Security
- Monitoring
- Containers
- DevOps
- Terraform
- High Availability
- Cost Optimization
- Real Interview Questions

---

# 🎯 Practice Challenge

Try answering all **53 interview questions** without referring to your notes.

If you can confidently answer most of them, you are well prepared for:

- AWS Cloud Engineer
- AWS DevOps Engineer
- Cloud Support Engineer
- Site Reliability Engineer (SRE)
- Junior Solutions Architect

---

# 🚀 What's Next?

In **Chapter 40 – AWS Cheat Sheet**, you'll get a quick revision guide containing:

- 📌 Important AWS Services
- 📌 CLI Commands
- 📌 Architecture Diagrams
- 📌 Networking Summary
- 📌 Storage Comparison
- 📌 Security Best Practices
- 📌 DevOps Commands
- 📌 Interview Revision Notes
