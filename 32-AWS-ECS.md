# AWS Notes
# Chapter 32 - Amazon Elastic Container Service (ECS)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is Amazon ECS?
2. Why Use Amazon ECS?
3. Container Orchestration
4. ECS Architecture
5. ECS Components
6. Launch Types
7. Task Definitions
8. Tasks
9. Services
10. Clusters
11. Networking
12. Load Balancer Integration
13. Auto Scaling
14. ECS with ECR
15. ECS with CloudWatch
16. AWS CLI Commands
17. Best Practices
18. Common Use Cases
19. Summary
20. Interview Questions
21. Practice Exercises
22. Mini Project
23. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon ECS
- Learn container orchestration
- Deploy Docker containers
- Manage ECS clusters and services
- Use ECS with ECR and Load Balancers
- Monitor ECS applications

---

# 📖 What is Amazon ECS?

**Amazon Elastic Container Service (Amazon ECS)** is a fully managed container orchestration service provided by AWS.

It helps you deploy, manage, and scale Docker containers without managing complex infrastructure.

Amazon ECS integrates seamlessly with AWS services like ECR, IAM, CloudWatch, ALB, and Auto Scaling.

---

# 💡 Why Use Amazon ECS?

Without ECS:

```text
Build Container

↓

Create Server

↓

Install Docker

↓

Deploy Container

↓

Manage Scaling Manually
```

With ECS:

```text
Build Container

↓

Push Image to ECR

↓

Deploy to ECS

↓

Automatic Scaling & Monitoring
```

Benefits:

- ✅ Fully managed
- ✅ Highly scalable
- ✅ Easy deployment
- ✅ AWS integration
- ✅ Secure container management

---

# 🐳 What is Container Orchestration?

Container orchestration automates the deployment, scaling, networking, and management of containers.

It helps:

- Deploy containers automatically
- Replace failed containers
- Scale applications
- Balance traffic
- Simplify operations

---

# 🏗️ Amazon ECS Architecture

```text
Developer
      │
      ▼
Docker Image
      │
      ▼
Amazon ECR
      │
      ▼
Amazon ECS Cluster
      │
 ┌────┴─────┐
 ▼          ▼
Service   Task
      │
      ▼
Running Containers
```

---

# 📦 ECS Components

Amazon ECS consists of:

- Cluster
- Task Definition
- Task
- Service
- Container
- Launch Type

---

# 🚀 Launch Types

## EC2 Launch Type

Containers run on EC2 instances managed by you.

Advantages:

- Full server control
- Custom AMIs
- GPU support

---

## AWS Fargate Launch Type

AWS manages the servers.

Advantages:

- No server management
- Serverless containers
- Easy scaling
- Pay only for usage

---

# 📄 Task Definition

A **Task Definition** is a blueprint for running containers.

It includes:

- Docker image
- CPU
- Memory
- Environment variables
- Ports
- Storage
- IAM Role

Example:

```text
Task Definition

├── Image
├── CPU
├── Memory
├── Port
└── Environment Variables
```

---

# ⚙️ Tasks

A **Task** is a running instance of a Task Definition.

Example:

```text
Task Definition

↓

Run Task

↓

Running Container
```

---

# 🌐 Services

An ECS Service ensures that the desired number of tasks are always running.

Benefits:

- Automatic recovery
- High availability
- Load balancer integration
- Auto Scaling

---

# 🏢 Clusters

A Cluster is a logical group of ECS resources.

Example:

```text
Production Cluster

├── Service A
├── Service B
└── Service C
```

One cluster can host multiple applications.

---

# 🌍 Networking

Amazon ECS supports:

- VPC
- Subnets
- Security Groups
- Elastic Network Interfaces (ENI)

Each task can receive its own private IP address.

---

# ⚖️ Load Balancer Integration

Amazon ECS integrates with:

- Application Load Balancer (ALB)
- Network Load Balancer (NLB)

Flow:

```text
User

↓

Load Balancer

↓

ECS Service

↓

Containers
```

Benefits:

- High availability
- Traffic distribution
- Health checks

---

# 📈 Auto Scaling

Amazon ECS supports automatic scaling based on:

- CPU Usage
- Memory Usage
- Request Count
- Custom CloudWatch Metrics

Benefits:

- Cost optimization
- High availability
- Better performance

---

# 📦 ECS with Amazon ECR

Deployment flow:

```text
Build Docker Image

↓

Push to Amazon ECR

↓

ECS Pulls Image

↓

Container Starts
```

---

# 📊 ECS with CloudWatch

CloudWatch provides:

- CPU utilization
- Memory usage
- Task status
- Logs
- Alarms
- Metrics

Useful for monitoring applications.

---

# 🏗️ ECS Deployment Flow

```text
Developer
      │
      ▼
Docker Build
      │
      ▼
Amazon ECR
      │
      ▼
Amazon ECS
      │
      ▼
Load Balancer
      │
      ▼
Users
```

---

# 💻 Useful AWS CLI Commands

## Create Cluster

```bash
aws ecs create-cluster \
--cluster-name production
```

---

## List Clusters

```bash
aws ecs list-clusters
```

---

## Register Task Definition

```bash
aws ecs register-task-definition
```

---

## Create Service

```bash
aws ecs create-service
```

---

## List Services

```bash
aws ecs list-services \
--cluster production
```

---

## Run Task

```bash
aws ecs run-task
```

---

## Stop Task

```bash
aws ecs stop-task
```

---

# 🏆 Best Practices

- ✅ Use Fargate for serverless workloads
- ✅ Store images in Amazon ECR
- ✅ Use IAM Roles for Tasks
- ✅ Enable CloudWatch Logs
- ✅ Use ALB for web applications
- ✅ Configure Auto Scaling
- ✅ Keep Task Definitions versioned
- ✅ Use private subnets for containers

---

# 🌍 Common Use Cases

| Scenario | ECS |
|----------|-----|
| Web Applications | ✅ |
| Microservices | ✅ |
| REST APIs | ✅ |
| Background Jobs | ✅ |
| Batch Processing | ✅ |
| CI/CD Deployments | ✅ |

---

# 📝 Key Takeaways

- Amazon ECS is AWS's managed container orchestration service.
- Supports EC2 and AWS Fargate launch types.
- Uses Task Definitions to deploy containers.
- Integrates with Amazon ECR, ALB, IAM, and CloudWatch.
- Supports Auto Scaling and High Availability.
- Ideal for Docker-based applications.

---

# 📋 Summary

In this chapter, you learned:

- Amazon ECS
- Container Orchestration
- ECS Components
- Clusters
- Task Definitions
- Tasks
- Services
- Launch Types
- Networking
- Load Balancers
- Auto Scaling
- ECR Integration
- CloudWatch Monitoring
- AWS CLI Commands

---

# ❓ Interview Questions

## Beginner

1. What is Amazon ECS?
2. What is container orchestration?
3. What is an ECS Cluster?
4. What is a Task Definition?
5. Difference between a Task and a Service?

---

## Intermediate

6. Explain ECS launch types.
7. What is AWS Fargate?
8. How does ECS integrate with ECR?
9. Why use an Application Load Balancer with ECS?
10. Explain Auto Scaling in ECS.

---

## Advanced

11. Design a highly available ECS architecture.
12. Compare ECS and Kubernetes.
13. How does ECS recover failed containers?
14. Explain IAM Roles for Tasks.
15. How would you deploy a production application using ECS?

---

# 🎯 Practice Exercises

## Exercise 1

Create an ECS Cluster.

---

## Exercise 2

Create a Task Definition.

---

## Exercise 3

Push a Docker image to Amazon ECR.

---

## Exercise 4

Deploy the image using Amazon ECS.

---

## Exercise 5

Enable Auto Scaling and CloudWatch monitoring.

---

# 🧩 Mini Project

Deploy a Docker-based web application using Amazon ECS.

Tasks:

- Create an ECR repository
- Build and push Docker image
- Create an ECS Cluster
- Register a Task Definition
- Create an ECS Service
- Configure an Application Load Balancer
- Verify the application

Commit your project:

```bash
git add .
git commit -m "Deploy application using Amazon ECS"
```

---

# 📚 Further Reading

- Amazon ECS Documentation
- AWS Fargate Documentation
- Amazon ECR Documentation
- CloudWatch Documentation
- ECS Best Practices Guide

---

# 🚀 What's Next?

In **Chapter 33 – Amazon EKS**, you'll learn:

- ☸️ What is Kubernetes?
- 🚀 Amazon EKS Overview
- 📦 Pods & Deployments
- 🖥️ Worker Nodes
- 🌐 Kubernetes Networking
- 📊 Monitoring
- 💻 kubectl & AWS CLI
- 🛠️ Deploying Applications on EKS
