# AWS Notes
# Chapter 31 - Amazon Elastic Container Registry (ECR)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is Amazon ECR?
2. Why Use Amazon ECR?
3. Docker Registry Basics
4. How Amazon ECR Works
5. Public vs Private Repositories
6. Repository Components
7. Image Lifecycle
8. Image Scanning
9. Image Tagging
10. Authentication
11. IAM Integration
12. ECR with ECS & EKS
13. ECR with CI/CD
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

- Understand Amazon ECR
- Create and manage container repositories
- Push and pull Docker images
- Secure repositories using IAM
- Scan images for vulnerabilities
- Integrate ECR with ECS, EKS, and CI/CD pipelines

---

# 📖 What is Amazon ECR?

**Amazon Elastic Container Registry (ECR)** is a fully managed Docker container image registry provided by AWS.

It allows developers to securely store, manage, version, and deploy container images.

Amazon ECR eliminates the need to manage your own Docker registry.

---

# 💡 Why Use Amazon ECR?

Without ECR:

```text
Developer

↓

Local Docker Images

↓

Manual Image Sharing

↓

Deployment Challenges
```

With Amazon ECR:

```text
Developer

↓

Build Docker Image

↓

Push to Amazon ECR

↓

Deploy to ECS / EKS / EC2
```

Benefits:

- ✅ Fully managed
- ✅ Highly available
- ✅ Secure
- ✅ Integrated with AWS
- ✅ Supports Docker & OCI images

---

# 🐳 What is a Container Image?

A container image is a package containing:

- Application code
- Runtime
- Libraries
- Dependencies
- Configuration

Example:

```text
Docker Image

├── Ubuntu
├── Python
├── Flask App
└── Required Libraries
```

---

# ⚙️ How Amazon ECR Works

```text
Developer

↓

Docker Build

↓

Docker Image

↓

Push to Amazon ECR

↓

Pull from ECS / EKS / EC2

↓

Application Runs
```

---

# 📦 Repository Types

## Private Repository

- Accessible only to authorized users
- Ideal for production applications
- IAM-controlled access

---

## Public Repository

- Anyone can pull images
- Useful for open-source projects
- Publicly accessible

---

# 📁 Repository Components

An ECR repository stores:

- Docker Images
- Image Tags
- Image Metadata
- Image Digests
- Scan Results

---

# 🏷️ Image Tags

Tags help identify image versions.

Example:

```text
my-app

├── latest
├── v1.0
├── v1.1
└── production
```

Example:

```bash
docker tag my-app:latest 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:v1
```

---

# 🔄 Image Lifecycle

```text
Build Image

↓

Tag Image

↓

Push to ECR

↓

Deploy

↓

Update Image

↓

Remove Old Images
```

---

# 🔍 Image Scanning

Amazon ECR can scan images for security vulnerabilities.

It detects:

- Vulnerable packages
- Known CVEs
- Security risks

Benefits:

- Secure deployments
- Compliance
- Early vulnerability detection

---

# 🔐 Authentication

Before pushing images, Docker must authenticate.

Login command:

```bash
aws ecr get-login-password \
| docker login \
--username AWS \
--password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
```

Authentication is managed using IAM credentials.

---

# 👤 IAM Integration

Amazon ECR integrates with IAM.

Permissions include:

- Create Repository
- Push Images
- Pull Images
- Delete Images
- Delete Repository

Use the Principle of Least Privilege.

---

# 🚀 ECR with ECS & EKS

Typical deployment flow:

```text
Developer

↓

Build Docker Image

↓

Push to ECR

↓

ECS / EKS Pulls Image

↓

Application Starts
```

Amazon ECS and Amazon EKS can directly pull images from ECR.

---

# 🔄 ECR with CI/CD

Amazon ECR integrates with:

- CodeCommit
- CodeBuild
- CodePipeline
- Jenkins
- GitHub Actions
- GitLab CI/CD

Pipeline:

```text
Code

↓

Build

↓

Docker Image

↓

Push to ECR

↓

Deploy
```

---

# 🏗️ Amazon ECR Architecture

```text
Developer
      │
      ▼
 Docker Build
      │
      ▼
 Amazon ECR Repository
      │
 ┌────┴─────┐
 ▼          ▼
Amazon ECS Amazon EKS
      │
      ▼
 Running Containers
```

---

# 💻 Useful AWS CLI Commands

## Create Repository

```bash
aws ecr create-repository \
--repository-name my-app
```

---

## List Repositories

```bash
aws ecr describe-repositories
```

---

## Delete Repository

```bash
aws ecr delete-repository \
--repository-name my-app
```

---

## List Images

```bash
aws ecr list-images \
--repository-name my-app
```

---

## Describe Images

```bash
aws ecr describe-images \
--repository-name my-app
```

---

## Delete Image

```bash
aws ecr batch-delete-image \
--repository-name my-app \
--image-ids imageTag=v1
```

---

# 🏆 Best Practices

- ✅ Use image tags for versioning
- ✅ Enable image scanning
- ✅ Remove unused images
- ✅ Use IAM roles for access
- ✅ Avoid using only `latest` tag
- ✅ Apply lifecycle policies
- ✅ Store images in the nearest AWS Region
- ✅ Automate builds using CI/CD

---

# 🌍 Common Use Cases

| Scenario | Amazon ECR |
|----------|------------|
| Docker Image Storage | ✅ |
| Kubernetes Deployments | ✅ |
| ECS Applications | ✅ |
| CI/CD Pipelines | ✅ |
| Image Versioning | ✅ |
| Secure Image Registry | ✅ |

---

# 📝 Key Takeaways

- Amazon ECR is a managed container image registry.
- Supports private and public repositories.
- Stores Docker and OCI images securely.
- Integrates with ECS, EKS, and CI/CD tools.
- Supports vulnerability scanning.
- Uses IAM for authentication and authorization.

---

# 📋 Summary

In this chapter, you learned:

- Amazon ECR
- Container Images
- Repositories
- Image Tags
- Image Lifecycle
- Image Scanning
- Authentication
- IAM Integration
- ECS & EKS Integration
- CI/CD Integration
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Amazon ECR?
2. Why do we use ECR?
3. What is a container image?
4. What is an image tag?
5. Difference between public and private repositories?

---

## Intermediate

6. Explain the image lifecycle.
7. How does ECR authenticate Docker?
8. What is image scanning?
9. Explain IAM integration with ECR.
10. How does ECS use ECR?

---

## Advanced

11. Explain an ECR-based CI/CD pipeline.
12. How do lifecycle policies work?
13. How would you secure an ECR repository?
14. Compare Amazon ECR with Docker Hub.
15. How does Amazon ECR integrate with Kubernetes?

---

# 🎯 Practice Exercises

## Exercise 1

Create an Amazon ECR repository.

---

## Exercise 2

Build a Docker image.

---

## Exercise 3

Tag the Docker image.

---

## Exercise 4

Push the image to Amazon ECR.

---

## Exercise 5

Deploy the image using Amazon ECS or Amazon EKS.

---

# 🧩 Mini Project

Create a Docker application and deploy it using Amazon ECR.

Tasks:

- Create an ECR repository
- Build a Docker image
- Push the image to ECR
- Pull the image on an EC2 instance
- Run the container
- Verify the application

Commit your project:

```bash
git add .
git commit -m "Deploy Docker application using Amazon ECR"
```

---

# 📚 Further Reading

- Amazon ECR Documentation
- Docker Documentation
- OCI Image Specification
- Amazon ECS Documentation
- Amazon EKS Documentation

---

# 🚀 What's Next?

In **Chapter 32 – Amazon ECS**, you'll learn:

- 🚢 What is Amazon ECS?
- 📦 ECS Components
- 🖥️ ECS Launch Types (EC2 & Fargate)
- 📋 Task Definitions
- ⚙️ Services & Clusters
- 🌐 Networking
- 📊 Monitoring
- 💻 AWS CLI Commands
- 🛠️ Hands-on Container Deployment
```
