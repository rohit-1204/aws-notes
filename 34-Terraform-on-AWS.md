# AWS Notes
# Chapter 34 - Terraform on AWS

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 5–6 hours

---

# 📚 Table of Contents

1. What is Terraform?
2. Why Use Terraform?
3. Infrastructure as Code (IaC)
4. Terraform Architecture
5. Installing Terraform
6. Terraform Workflow
7. Terraform Configuration Files
8. Providers
9. Resources
10. Variables
11. Outputs
12. Terraform State
13. Modules
14. Terraform with AWS
15. Common AWS Resources
16. Useful Terraform Commands
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

- Understand Infrastructure as Code (IaC)
- Learn Terraform fundamentals
- Deploy AWS infrastructure using Terraform
- Manage Terraform state
- Organize infrastructure using modules
- Follow Terraform best practices

---

# 📖 What is Terraform?

**Terraform** is an open-source **Infrastructure as Code (IaC)** tool developed by **HashiCorp**.

It allows you to create, update, and manage cloud infrastructure using configuration files instead of manually creating resources.

Terraform supports AWS, Azure, Google Cloud, Kubernetes, VMware, GitHub, and many other providers.

---

# 💡 Why Use Terraform?

Without Terraform:

```text
Developer

↓

AWS Console

↓

Manual Configuration

↓

Time Consuming

↓

Human Errors
```

With Terraform:

```text
Developer

↓

Terraform Code

↓

terraform apply

↓

AWS Infrastructure Created
```

Benefits:

- ✅ Infrastructure as Code
- ✅ Automation
- ✅ Version Control
- ✅ Repeatable Deployments
- ✅ Easy Rollback

---

# 🏗️ Infrastructure as Code (IaC)

Infrastructure as Code means managing infrastructure using code.

Instead of manually creating resources:

- EC2
- VPC
- RDS
- IAM
- S3

You write Terraform configuration files.

Benefits:

- Consistency
- Automation
- Faster deployments
- Reduced errors

---

# 🏛️ Terraform Architecture

```text
Terraform Configuration (.tf)

↓

Terraform CLI

↓

AWS Provider

↓

AWS API

↓

AWS Resources
```

---

# 💻 Installing Terraform

Install Terraform on:

- Linux
- Windows
- macOS

Verify installation:

```bash
terraform version
```

---

# 🔄 Terraform Workflow

Terraform follows a simple workflow:

```text
Write Code

↓

terraform init

↓

terraform plan

↓

terraform apply

↓

Infrastructure Created

↓

terraform destroy
```

---

# 📄 Terraform Configuration Files

Terraform uses **.tf** files.

Common files:

```text
main.tf

variables.tf

outputs.tf

provider.tf

terraform.tfvars
```

---

# 🌐 Providers

A Provider allows Terraform to communicate with cloud platforms.

Example providers:

- AWS
- Azure
- Google Cloud
- Kubernetes
- Docker

Example:

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

---

# 📦 Resources

Resources define the infrastructure you want to create.

Examples:

- EC2 Instance
- VPC
- S3 Bucket
- Security Group
- IAM Role

Example:

```hcl
resource "aws_instance" "web" {
  ami           = "ami-xxxxxxxx"
  instance_type = "t2.micro"
}
```

---

# 📝 Variables

Variables make Terraform code reusable.

Example:

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

Benefits:

- Reusable code
- Easy customization
- Better maintenance

---

# 📤 Outputs

Outputs display useful information after deployment.

Example:

```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

Example output:

```text
Public IP:
13.234.xxx.xxx
```

---

# 💾 Terraform State

Terraform stores infrastructure information in a **State File**.

Default file:

```text
terraform.tfstate
```

Purpose:

- Track resources
- Detect changes
- Plan updates

For teams, use a **remote backend** such as Amazon S3.

---

# 📂 Modules

Modules help organize reusable Terraform code.

Example:

```text
modules/

├── ec2/
├── vpc/
├── rds/
└── security-group/
```

Benefits:

- Reusability
- Cleaner code
- Easier maintenance

---

# ☁️ Terraform with AWS

Terraform can create almost every AWS service.

Common resources:

- Amazon EC2
- Amazon VPC
- Amazon S3
- Amazon IAM
- Amazon RDS
- Amazon EKS
- Amazon ECS
- Amazon Lambda
- Route 53

---

# 🏗️ Example Deployment Flow

```text
Developer

↓

Terraform Files

↓

Terraform CLI

↓

AWS Provider

↓

AWS Resources

↓

Running Infrastructure
```

---

# 💻 Useful Terraform Commands

## Initialize Project

```bash
terraform init
```

---

## Validate Configuration

```bash
terraform validate
```

---

## Format Code

```bash
terraform fmt
```

---

## Preview Changes

```bash
terraform plan
```

---

## Create Infrastructure

```bash
terraform apply
```

---

## Show Current Resources

```bash
terraform show
```

---

## List Resources

```bash
terraform state list
```

---

## Destroy Infrastructure

```bash
terraform destroy
```

---

# 🏆 Best Practices

- ✅ Store code in Git
- ✅ Use remote state in Amazon S3
- ✅ Enable state locking
- ✅ Use variables instead of hardcoding values
- ✅ Organize code using modules
- ✅ Run `terraform plan` before `apply`
- ✅ Use meaningful resource names
- ✅ Follow the Principle of Least Privilege

---

# 🌍 Common Use Cases

| Scenario | Terraform |
|----------|-----------|
| EC2 Deployment | ✅ |
| VPC Creation | ✅ |
| Kubernetes Infrastructure | ✅ |
| Multi-Environment Setup | ✅ |
| CI/CD Automation | ✅ |
| Disaster Recovery | ✅ |

---

# 📝 Key Takeaways

- Terraform is an Infrastructure as Code tool.
- Uses declarative configuration files.
- Supports multiple cloud providers.
- Automates AWS infrastructure deployment.
- Stores infrastructure state.
- Modules improve code reusability.
- Widely used in DevOps.

---

# 📋 Summary

In this chapter, you learned:

- Terraform
- Infrastructure as Code
- Providers
- Resources
- Variables
- Outputs
- State File
- Modules
- AWS Integration
- Terraform Workflow
- CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Terraform?
2. What is Infrastructure as Code?
3. What is a Provider?
4. What is a Resource?
5. What is Terraform State?

---

## Intermediate

6. Explain the Terraform workflow.
7. Why are Variables used?
8. What are Modules?
9. Why is remote state important?
10. Explain `terraform plan`.

---

## Advanced

11. Design a production-ready Terraform project.
12. Explain state locking.
13. How does Terraform detect infrastructure changes?
14. Compare Terraform and AWS CloudFormation.
15. Explain Terraform modules with an example.

---

# 🎯 Practice Exercises

## Exercise 1

Install Terraform.

---

## Exercise 2

Configure the AWS Provider.

---

## Exercise 3

Create an EC2 instance using Terraform.

---

## Exercise 4

Create an S3 bucket.

---

## Exercise 5

Destroy all created resources.

---

# 🧩 Mini Project

Deploy a complete AWS infrastructure using Terraform.

Include:

- VPC
- Public Subnet
- Internet Gateway
- Security Group
- EC2 Instance
- S3 Bucket

Commit your project:

```bash
git add .
git commit -m "Deploy AWS infrastructure using Terraform"
```

---

# 📚 Further Reading

- Terraform Documentation
- Terraform AWS Provider Documentation
- HashiCorp Learn
- AWS Well-Architected Framework
- Terraform Module Registry

---

# 🚀 What's Next?

In **Chapter 35 – AWS Monitoring and Logging**, you'll learn:

- 📊 CloudWatch Metrics
- 📝 CloudWatch Logs
- 🚨 CloudWatch Alarms
- 📈 Dashboards
- 📜 AWS CloudTrail
- 🔍 Log Analysis
- 📢 SNS Notifications
- 🛠️ Monitoring Best Practices
