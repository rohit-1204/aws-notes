# AWS Notes
# Chapter 40 - AWS Cheat Sheet

> 📘 **Level:** Beginner to Advanced
> ⏱️ **Reading Time:** 30–45 minutes
> 🛠️ **Purpose:** Quick Revision Before Interviews & Certification

---

# 📚 Table of Contents

1. AWS Global Infrastructure
2. Core AWS Services
3. Compute Services
4. Storage Services
5. Networking Services
6. Database Services
7. Security Services
8. Monitoring Services
9. Containers & DevOps
10. Infrastructure as Code
11. Common AWS CLI Commands
12. Architecture Flow
13. Important Ports
14. Best Practices
15. Interview Revision
16. AWS Service Comparison
17. Key Takeaways

---

# 🌍 AWS Global Infrastructure

```
Region
   │
   ├── Availability Zone (AZ)
   │       │
   │       ├── Data Center
   │       └── Data Center
   │
   └── Availability Zone (AZ)
```

- 🌎 Region = Geographic Location
- 🏢 AZ = One or More Data Centers
- 🌐 Edge Location = CDN (CloudFront)

---

# ☁️ Core AWS Services

| Category | Service |
|----------|----------|
| Compute | EC2, Lambda, ECS, EKS |
| Storage | S3, EBS, EFS |
| Database | RDS, DynamoDB |
| Networking | VPC, Route 53, ELB |
| Security | IAM, KMS, Secrets Manager |
| Monitoring | CloudWatch, CloudTrail |
| DevOps | CodePipeline, CodeBuild, CodeDeploy |
| IaC | CloudFormation, Terraform |

---

# 🖥️ Compute Services

### EC2

- Virtual Machine
- Full OS Access
- Persistent
- Auto Scaling Supported

---

### Lambda

- Serverless
- Pay per Execution
- Event Driven
- No Server Management

---

### ECS

- Container Orchestration
- AWS Native
- Docker Support

---

### EKS

- Managed Kubernetes
- Production Container Platform

---

# 💾 Storage Services

| Service | Storage Type |
|----------|--------------|
| S3 | Object Storage |
| EBS | Block Storage |
| EFS | File Storage |

---

### Storage Comparison

| Service | Attach To |
|----------|-----------|
| EBS | One EC2 |
| EFS | Multiple EC2 |
| S3 | Internet/API |

---

# 🌐 Networking Services

### VPC

Private Network

---

### Subnet

Logical Network inside VPC

- Public
- Private

---

### Internet Gateway

Provides Internet Access

---

### NAT Gateway

Private Instances → Internet

Internet ❌ → Private Instances

---

### Route Table

Controls Traffic Routing

---

### Security Group

- Stateful
- Allow Only
- Instance Level

---

### Network ACL

- Stateless
- Allow & Deny
- Subnet Level

---

### Route 53

Managed DNS Service

---

### Elastic Load Balancer

Traffic Distribution

- ALB
- NLB
- GWLB

---

# 🗄️ Database Services

### Amazon RDS

Managed SQL Database

Supports:

- MySQL
- PostgreSQL
- MariaDB
- Oracle
- SQL Server

---

### DynamoDB

- NoSQL Database
- Serverless
- High Performance

---

# 🔐 Security Services

### IAM

Identity & Access Management

Components:

- Users
- Groups
- Roles
- Policies

---

### KMS

Encryption Key Management

---

### Secrets Manager

Stores:

- Passwords
- API Keys
- Tokens

---

### AWS Shield

DDoS Protection

---

### AWS WAF

Web Application Firewall

---

# 📊 Monitoring Services

### CloudWatch

- Metrics
- Logs
- Alarms
- Dashboards

---

### CloudTrail

Records AWS API Calls

---

### AWS Config

Tracks Configuration Changes

---

### SNS

Notifications

- Email
- SMS
- HTTP

---

# 📦 Containers & DevOps

### Amazon ECR

Docker Image Registry

---

### Amazon ECS

Container Service

---

### Amazon EKS

Managed Kubernetes

---

### CI/CD Services

```
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

# 🏗️ Infrastructure as Code

### CloudFormation

AWS Native IaC

Uses:

- YAML
- JSON

---

### Terraform

Multi-Cloud IaC

Uses:

- HCL

---

# 💻 Common AWS CLI Commands

## Configure CLI

```bash
aws configure
```

---

## List EC2 Instances

```bash
aws ec2 describe-instances
```

---

## List S3 Buckets

```bash
aws s3 ls
```

---

## List IAM Users

```bash
aws iam list-users
```

---

## List RDS Instances

```bash
aws rds describe-db-instances
```

---

## List Lambda Functions

```bash
aws lambda list-functions
```

---

## List CloudFormation Stacks

```bash
aws cloudformation list-stacks
```

---

## List EKS Clusters

```bash
aws eks list-clusters
```

---

## List ECS Clusters

```bash
aws ecs list-clusters
```

---

# 🏗️ AWS Production Architecture

```
                 Users
                    │
                    ▼
               Route 53
                    │
                    ▼
        Application Load Balancer
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
      EC2 AZ-1           EC2 AZ-2
          │                   │
          └─────────┬─────────┘
                    ▼
              Amazon RDS
               (Multi-AZ)
                    │
                    ▼
               Amazon S3

CloudWatch + CloudTrail + SNS
```

---

# 🔌 Common Ports

| Port | Service |
|------|----------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 27017 | MongoDB |

---

# 🏆 AWS Best Practices

- ✅ Enable MFA
- ✅ Use IAM Roles
- ✅ Follow Least Privilege
- ✅ Encrypt Data with KMS
- ✅ Store Secrets in Secrets Manager
- ✅ Enable CloudTrail
- ✅ Monitor using CloudWatch
- ✅ Enable Auto Scaling
- ✅ Use Multi-AZ Deployments
- ✅ Take Regular Backups
- ✅ Use Infrastructure as Code
- ✅ Tag AWS Resources

---

# 🎯 Interview Revision

### Difference Between

| Service A | Service B |
|------------|------------|
| ECS | EKS |
| EBS | EFS |
| EBS | S3 |
| ALB | NLB |
| Security Group | NACL |
| IAM User | IAM Role |
| CloudWatch | CloudTrail |
| RDS | DynamoDB |
| CloudFormation | Terraform |
| Lambda | EC2 |

---

# 📝 AWS Well-Architected Pillars

- 🏗️ Operational Excellence
- 🔒 Security
- 🏎️ Performance Efficiency
- 💰 Cost Optimization
- 🌍 Reliability
- ♻️ Sustainability

---

# 🚀 DevOps Pipeline

```
Developer

↓

Git Push

↓

CodeCommit

↓

CodeBuild

↓

Unit Testing

↓

CodeDeploy

↓

CodePipeline

↓

Production
```

---

# 📌 Key Takeaways

- EC2 = Virtual Machines
- Lambda = Serverless Computing
- S3 = Object Storage
- EBS = Block Storage
- EFS = Shared File Storage
- VPC = Private Network
- Route 53 = DNS
- ALB = HTTP/HTTPS Load Balancer
- IAM = Access Management
- KMS = Encryption
- CloudWatch = Monitoring
- CloudTrail = API Auditing
- ECS = Containers
- EKS = Kubernetes
- CloudFormation = AWS IaC
- Terraform = Multi-Cloud IaC

---

# 🎯 Final Revision Checklist

## AWS Fundamentals

- ✅ Regions & AZs
- ✅ Shared Responsibility Model
- ✅ IAM
- ✅ Billing

---

## Compute

- ✅ EC2
- ✅ Auto Scaling
- ✅ Lambda
- ✅ ECS
- ✅ EKS

---

## Storage

- ✅ S3
- ✅ EBS
- ✅ EFS

---

## Networking

- ✅ VPC
- ✅ Subnets
- ✅ Route Tables
- ✅ Internet Gateway
- ✅ NAT Gateway
- ✅ Security Groups
- ✅ NACL
- ✅ Route 53
- ✅ Load Balancer

---

## Database

- ✅ RDS
- ✅ DynamoDB

---

## Security

- ✅ IAM
- ✅ KMS
- ✅ Secrets Manager
- ✅ WAF
- ✅ Shield

---

## Monitoring

- ✅ CloudWatch
- ✅ CloudTrail
- ✅ AWS Config
- ✅ SNS

---

## DevOps

- ✅ ECR
- ✅ ECS
- ✅ EKS
- ✅ CodePipeline
- ✅ CloudFormation
- ✅ Terraform

---

# 🎉 Congratulations!

You have completed the **AWS for DevOps Engineer** learning path.

You now have knowledge of:

- ☁️ AWS Cloud Fundamentals
- 🌐 Networking
- 💻 Compute
- 💾 Storage
- 🗄️ Databases
- 🔐 Security
- 📊 Monitoring
- 🐳 Containers
- 🚀 DevOps
- 🏗️ Infrastructure as Code
- 📈 Production Architecture
- 💼 Interview Preparation

**Next Goal:** Build real-world AWS projects, automate deployments with Terraform and CI/CD, and prepare for the **AWS Certified Developer**, **AWS Certified SysOps Administrator**, or **AWS Certified DevOps Engineer – Professional** certification.
