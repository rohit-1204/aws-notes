# AWS Notes
# Chapter 33 - Amazon Elastic Kubernetes Service (EKS)

> 📘 **Level:** Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–6 hours

---

# 📚 Table of Contents

1. What is Amazon EKS?
2. Why Use Amazon EKS?
3. What is Kubernetes?
4. EKS Architecture
5. Kubernetes Components
6. Worker Nodes
7. Pods
8. Deployments
9. Services
10. Namespaces
11. ConfigMaps & Secrets
12. EKS Networking
13. EKS with IAM
14. EKS with ECR
15. Auto Scaling
16. Monitoring
17. AWS CLI & kubectl Commands
18. Best Practices
19. Common Use Cases
20. Summary
21. Interview Questions
22. Practice Exercises
23. Mini Project
24. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon EKS
- Learn Kubernetes fundamentals
- Deploy applications on Kubernetes
- Manage Pods and Deployments
- Configure networking and IAM
- Monitor Kubernetes workloads

---

# 📖 What is Amazon EKS?

**Amazon Elastic Kubernetes Service (Amazon EKS)** is a fully managed Kubernetes service provided by AWS.

AWS manages the Kubernetes control plane, while you manage your applications and worker nodes (or use AWS Fargate).

Amazon EKS simplifies running Kubernetes in production.

---

# 💡 Why Use Amazon EKS?

Without EKS:

```text
Install Kubernetes

↓

Manage Control Plane

↓

Upgrade Cluster

↓

Maintain High Availability

↓

Deploy Applications
```

With Amazon EKS:

```text
Create EKS Cluster

↓

Deploy Applications

↓

AWS Manages Control Plane

↓

Automatic Scaling & High Availability
```

Benefits:

- ✅ Managed Kubernetes
- ✅ Highly Available
- ✅ Secure
- ✅ Scalable
- ✅ Integrated with AWS Services

---

# ☸️ What is Kubernetes?

Kubernetes (K8s) is an open-source container orchestration platform.

It automates:

- Container deployment
- Scaling
- Load balancing
- Self-healing
- Rolling updates

---

# 🏗️ Amazon EKS Architecture

```text
Developer
      │
      ▼
 kubectl / AWS CLI
      │
      ▼
 Amazon EKS Control Plane
      │
 ┌────┴─────┐
 ▼          ▼
Worker Node Worker Node
      │
      ▼
Pods (Containers)
```

---

# 📦 Kubernetes Components

Core components:

- Cluster
- Control Plane
- Worker Nodes
- Pods
- Deployments
- Services
- Namespaces
- ConfigMaps
- Secrets

---

# 🖥️ Worker Nodes

Worker Nodes are EC2 instances or AWS Fargate resources where containers run.

Responsibilities:

- Run Pods
- Pull container images
- Execute workloads
- Communicate with the control plane

---

# 📦 Pods

A **Pod** is the smallest deployable unit in Kubernetes.

A Pod can contain:

- One container
- Multiple related containers

Example:

```text
Pod

├── Nginx Container
└── Sidecar Container
```

---

# 🚀 Deployments

A Deployment manages Pods.

Features:

- Rolling updates
- Rollbacks
- Replica management
- Self-healing

Example:

```text
Deployment

↓

ReplicaSet

↓

Pods
```

---

# 🌐 Services

A Kubernetes Service exposes Pods to users or other applications.

Types:

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

---

# 📂 Namespaces

Namespaces logically separate Kubernetes resources.

Examples:

```text
default

development

testing

production
```

Useful for multi-team environments.

---

# 🔐 ConfigMaps & Secrets

### ConfigMaps

Store non-sensitive configuration.

Examples:

- URLs
- Environment variables
- Application settings

---

### Secrets

Store sensitive information.

Examples:

- Database passwords
- API Keys
- Certificates
- Tokens

---

# 🌍 EKS Networking

Amazon EKS integrates with:

- VPC
- Subnets
- Security Groups
- Elastic Network Interfaces (ENI)

Each Pod receives its own IP address using the AWS VPC CNI plugin.

---

# 👤 EKS with IAM

IAM integrates with EKS for authentication and authorization.

Common features:

- IAM Roles
- IAM Users
- IAM Roles for Service Accounts (IRSA)

Benefits:

- Secure access
- Fine-grained permissions
- AWS resource integration

---

# 📦 EKS with Amazon ECR

Deployment workflow:

```text
Docker Build

↓

Amazon ECR

↓

Amazon EKS

↓

Pods Pull Images

↓

Application Runs
```

---

# 📈 Auto Scaling

Amazon EKS supports:

- Cluster Autoscaler
- Horizontal Pod Autoscaler (HPA)
- Vertical Pod Autoscaler (VPA)

Benefits:

- Automatic scaling
- Cost optimization
- High availability

---

# 📊 Monitoring

Amazon EKS integrates with:

- Amazon CloudWatch
- Prometheus
- Grafana
- AWS X-Ray

Monitor:

- CPU
- Memory
- Pod health
- Cluster health
- Logs

---

# 🏗️ EKS Deployment Flow

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
Amazon EKS
      │
      ▼
Pods
      │
      ▼
Users
```

---

# 💻 Useful AWS CLI & kubectl Commands

## Create Cluster

```bash
eksctl create cluster --name production
```

---

## List Nodes

```bash
kubectl get nodes
```

---

## List Pods

```bash
kubectl get pods
```

---

## List Deployments

```bash
kubectl get deployments
```

---

## List Services

```bash
kubectl get services
```

---

## Apply Configuration

```bash
kubectl apply -f deployment.yaml
```

---

## Delete Deployment

```bash
kubectl delete deployment nginx
```

---

# 🏆 Best Practices

- ✅ Use Amazon ECR for container images
- ✅ Use IAM Roles for Service Accounts (IRSA)
- ✅ Separate workloads using Namespaces
- ✅ Store secrets in Kubernetes Secrets
- ✅ Enable Cluster Autoscaler
- ✅ Monitor using CloudWatch and Prometheus
- ✅ Keep Kubernetes versions updated
- ✅ Use private subnets for worker nodes

---

# 🌍 Common Use Cases

| Scenario | Amazon EKS |
|----------|------------|
| Microservices | ✅ |
| Kubernetes Applications | ✅ |
| Web Applications | ✅ |
| CI/CD Pipelines | ✅ |
| Machine Learning | ✅ |
| Enterprise Applications | ✅ |

---

# 📝 Key Takeaways

- Amazon EKS is AWS's managed Kubernetes service.
- AWS manages the Kubernetes control plane.
- Pods are the smallest deployment units.
- Deployments manage Pods automatically.
- Supports Auto Scaling and High Availability.
- Integrates with Amazon ECR, IAM, CloudWatch, and VPC.

---

# 📋 Summary

In this chapter, you learned:

- Amazon EKS
- Kubernetes Basics
- Control Plane
- Worker Nodes
- Pods
- Deployments
- Services
- Namespaces
- ConfigMaps
- Secrets
- Networking
- IAM Integration
- Auto Scaling
- Monitoring
- kubectl Commands

---

# ❓ Interview Questions

## Beginner

1. What is Amazon EKS?
2. What is Kubernetes?
3. What is a Pod?
4. What is a Deployment?
5. What is a Kubernetes Service?

---

## Intermediate

6. Explain the EKS architecture.
7. Difference between ECS and EKS.
8. What are Namespaces?
9. What are ConfigMaps and Secrets?
10. Explain Cluster Autoscaler.

---

## Advanced

11. Design a production-ready EKS architecture.
12. Explain IAM Roles for Service Accounts (IRSA).
13. How does EKS integrate with Amazon ECR?
14. Explain Kubernetes networking in AWS.
15. How would you secure an EKS cluster?

---

# 🎯 Practice Exercises

## Exercise 1

Create an Amazon EKS cluster.

---

## Exercise 2

Deploy an Nginx application.

---

## Exercise 3

Scale the deployment.

---

## Exercise 4

Expose the application using a LoadBalancer Service.

---

## Exercise 5

Monitor the cluster using CloudWatch.

---

# 🧩 Mini Project

Deploy a Kubernetes application on Amazon EKS.

Tasks:

- Create an EKS Cluster
- Build a Docker image
- Push the image to Amazon ECR
- Create Deployment and Service YAML files
- Deploy the application
- Verify access through the LoadBalancer
- Enable monitoring

Commit your project:

```bash
git add .
git commit -m "Deploy Kubernetes application using Amazon EKS"
```

---

# 📚 Further Reading

- Amazon EKS Documentation
- Kubernetes Documentation
- kubectl Cheat Sheet
- Amazon ECR Documentation
- Kubernetes Best Practices

---

# 🚀 What's Next?

In **Chapter 34 – Terraform on AWS**, you'll learn:

- 🌍 Infrastructure as Code (IaC)
- 🏗️ Terraform Basics
- 📦 Providers & Resources
- 📄 Variables & Outputs
- 📂 State Management
- ☁️ Deploying AWS Infrastructure
- 🔄 Terraform Workflow
- 🛠️ Hands-on AWS Infrastructure Automation
