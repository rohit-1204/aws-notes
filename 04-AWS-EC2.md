# AWS Notes
# Chapter 04 - Amazon EC2 (Elastic Compute Cloud)

> **Level:** Beginner to Intermediate
> **Estimated Reading Time:** 75–90 minutes
> **Practice Time:** 3–4 hours

---

# Table of Contents

1. Introduction to Amazon EC2
2. Why Use EC2?
3. EC2 Features
4. EC2 Pricing Models
5. EC2 Instance Types
6. Amazon Machine Images (AMI)
7. EC2 Instance Lifecycle
8. Launching an EC2 Instance
9. Key Pairs
10. Security Groups
11. Elastic IP Address
12. User Data
13. Connecting to EC2
14. EC2 Storage Overview
15. Monitoring EC2
16. AWS CLI Commands
17. EC2 Best Practices
18. Common EC2 Scenarios
19. Summary
20. Interview Questions
21. Practice Exercises
22. Mini Project
23. Further Reading

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon EC2
- Launch and manage EC2 instances
- Choose the correct instance type
- Understand AMIs
- Configure Security Groups
- Connect to EC2 using SSH
- Use Elastic IPs
- Automate provisioning with User Data
- Manage EC2 using the AWS CLI

---

# What is Amazon EC2?

Amazon Elastic Compute Cloud (EC2) is a web service that provides resizable virtual servers in the cloud.

Instead of purchasing physical servers, you can launch virtual machines (instances) within minutes.

EC2 allows you to:

- Run applications
- Host websites
- Deploy databases
- Build development environments
- Run containers
- Scale workloads on demand

---

# Why Use EC2?

Amazon EC2 offers:

- On-demand virtual machines
- Flexible instance sizes
- Global deployment
- Auto Scaling
- Pay-as-you-go pricing
- Integration with AWS services
- High availability

---

# EC2 Architecture

```text
                    Internet
                        │
                        ▼
                Security Group
                        │
                        ▼
                  EC2 Instance
                        │
         ┌──────────────┼──────────────┐
         │              │              │
         ▼              ▼              ▼
       EBS            IAM Role      CloudWatch
```

---

# EC2 Features

- Virtual Machines
- Multiple Operating Systems
- Elastic Scaling
- Multiple CPU and Memory Options
- Secure Networking
- Load Balancer Integration
- Monitoring with CloudWatch
- IAM Role Integration

---

# EC2 Pricing Models

## On-Demand

Pay only for the time you use.

Best for:

- Development
- Testing
- Short-term workloads

---

## Reserved Instances

Commit for 1 or 3 years.

Benefits:

- Lower cost
- Predictable workloads

---

## Spot Instances

Use unused AWS capacity.

Benefits:

- Up to 90% cheaper

Limitations:

- AWS can terminate the instance anytime.

Suitable for:

- Batch processing
- CI/CD
- Big data

---

## Dedicated Hosts

Physical servers dedicated to one customer.

Suitable for:

- Licensing requirements
- Compliance

---

# EC2 Instance Types

AWS offers different instance families.

| Family | Purpose |
|---------|----------|
| t3, t4g | General Purpose |
| m5, m6 | Balanced Compute & Memory |
| c5, c6 | Compute Optimized |
| r5, r6 | Memory Optimized |
| i3, i4 | Storage Optimized |
| p4, g5 | GPU / Machine Learning |

---

# Understanding Instance Names

Example:

```
t3.medium
```

| Part | Meaning |
|------|---------|
| t | Instance Family |
| 3 | Generation |
| medium | Size |

---

# Amazon Machine Image (AMI)

An AMI is a template used to launch an EC2 instance.

It includes:

- Operating System
- Installed Software
- Configuration
- Storage Mapping

Examples:

- Ubuntu
- Amazon Linux
- Red Hat
- Windows Server

---

# EC2 Instance Lifecycle

```text
Pending
   │
   ▼
Running
   │
 ┌─┴────────────┐
 ▼              ▼
Stopped     Rebooting
 │
 ▼
Running
 │
 ▼
Terminated
```

---

# Launching an EC2 Instance

Steps:

1. Open EC2 Dashboard.
2. Click **Launch Instance**.
3. Choose an AMI.
4. Select an Instance Type.
5. Configure Key Pair.
6. Configure Network.
7. Configure Security Group.
8. Review settings.
9. Launch the instance.

---

# Key Pairs

A Key Pair is used for secure SSH authentication.

It consists of:

- Public Key (stored by AWS)
- Private Key (downloaded by you)

Example:

```text
my-key.pem
```

Set proper permissions:

```bash
chmod 400 my-key.pem
```

---

# Security Groups

A Security Group acts as a virtual firewall for EC2.

It controls:

- Inbound traffic
- Outbound traffic

Example Rules:

| Port | Protocol | Purpose |
|------|----------|----------|
| 22 | SSH | Remote Login |
| 80 | HTTP | Web Traffic |
| 443 | HTTPS | Secure Web Traffic |

---

# Elastic IP Address

An Elastic IP is a static public IPv4 address.

Benefits:

- Persistent public IP
- Survives instance stop/start (when re-associated)
- Easy DNS mapping

Use Elastic IPs only when necessary.

---

# User Data

User Data allows commands or scripts to run automatically during the first boot.

Example:

```bash
#!/bin/bash
apt update
apt install nginx -y
systemctl enable nginx
systemctl start nginx
```

Use cases:

- Install packages
- Configure servers
- Deploy applications

---

# Connecting to EC2

## Linux / macOS

```bash
ssh -i my-key.pem ubuntu@<public-ip>
```

Example:

```bash
ssh -i my-key.pem ubuntu@54.201.10.20
```

---

## Windows

Use:

- PuTTY
- Windows OpenSSH
- EC2 Instance Connect (supported AMIs)

---

# EC2 Storage Overview

Common storage options:

| Storage | Description |
|----------|-------------|
| EBS | Persistent Block Storage |
| Instance Store | Temporary Storage |
| EFS | Shared Network File System |
| S3 | Object Storage |

---

# Monitoring EC2

CloudWatch provides metrics such as:

- CPU Utilization
- Network In
- Network Out
- Disk Read/Write
- Status Checks

You can create alarms for resource usage.

---

# Useful AWS CLI Commands

List EC2 instances:

```bash
aws ec2 describe-instances
```

Start an instance:

```bash
aws ec2 start-instances --instance-ids i-1234567890abcdef0
```

Stop an instance:

```bash
aws ec2 stop-instances --instance-ids i-1234567890abcdef0
```

Reboot an instance:

```bash
aws ec2 reboot-instances --instance-ids i-1234567890abcdef0
```

Terminate an instance:

```bash
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0
```

Describe available instance types:

```bash
aws ec2 describe-instance-types
```

---

# EC2 Best Practices

✔ Use IAM Roles instead of Access Keys.

✔ Enable detailed monitoring when needed.

✔ Use Security Groups with least privilege.

✔ Use Elastic IPs only if required.

✔ Regularly create AMI backups.

✔ Use User Data for automation.

✔ Tag resources properly.

✔ Stop unused instances to save costs.

---

# Common EC2 Scenarios

| Scenario | Solution |
|----------|----------|
| Host a website | EC2 + Security Group + EBS |
| CI/CD Build Server | EC2 + IAM Role |
| Application Server | EC2 + Load Balancer |
| Auto Scaling Web App | EC2 + Auto Scaling Group |
| Development Environment | EC2 On-Demand Instance |

---

# Key Takeaways

- EC2 provides scalable virtual machines.
- AMIs are templates for launching instances.
- Security Groups protect EC2 instances.
- Key Pairs provide secure SSH access.
- User Data automates instance configuration.
- CloudWatch monitors instance health.
- Choose the right pricing model based on workload.

---

# Summary

In this chapter, you learned:

- Amazon EC2
- EC2 Features
- Pricing Models
- Instance Types
- Amazon Machine Images
- Instance Lifecycle
- Key Pairs
- Security Groups
- Elastic IP
- User Data
- Connecting to EC2
- EC2 Storage
- CloudWatch Monitoring
- AWS CLI Commands
- Best Practices

---

# Interview Questions

## Beginner

1. What is Amazon EC2?
2. What is an EC2 Instance?
3. What is an AMI?
4. What is a Security Group?
5. What is a Key Pair?

---

## Intermediate

6. Explain the EC2 Instance Lifecycle.
7. What is User Data?
8. What is the difference between EBS and Instance Store?
9. What are the EC2 pricing models?
10. What is an Elastic IP?

---

## Advanced

11. How would you secure an EC2 instance?
12. When would you use Spot Instances?
13. Explain how EC2 integrates with IAM Roles.
14. How would you automate EC2 provisioning?

---

# Practice Exercises

## Exercise 1

Launch an Ubuntu EC2 instance using the AWS Console.

---

## Exercise 2

Create a Security Group that allows:

- SSH (22)
- HTTP (80)
- HTTPS (443)

---

## Exercise 3

Connect to the EC2 instance using SSH.

---

## Exercise 4

Create a User Data script to install Nginx automatically.

---

## Exercise 5

Use the AWS CLI to:

- List instances
- Stop an instance
- Start it again

---

# Mini Project

Create a Markdown file named:

```text
ec2-deployment-guide.md
```

Include:

- EC2 Architecture Diagram
- EC2 Pricing Models
- Instance Types
- Launch Steps
- Security Group Configuration
- User Data Script
- AWS CLI Commands
- EC2 Best Practices

Commit the file to Git:

```bash
git add .
git commit -m "Add Amazon EC2 deployment guide"
```

---

# Further Reading

- Amazon EC2 User Guide
- EC2 Instance Types
- Amazon Machine Images (AMI)
- EC2 Pricing
- EC2 Best Practices
- AWS CLI EC2 Reference

---

# What's Next?

In **Chapter 05 – Amazon EBS (Elastic Block Store)**, you'll learn:

- What is Amazon EBS?
- EBS Volume Types
- Snapshots
- Encryption
- Volume Attachment
- Resizing Volumes
- Performance Optimization
- Hands-on EBS Management
- AWS CLI Commands
- Best Practices
