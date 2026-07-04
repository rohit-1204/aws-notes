# AWS Notes
# Chapter 22 - AWS Systems Manager (SSM)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 90–120 minutes
> 🛠️ **Practice Time:** 5–6 hours

---

# 📚 Table of Contents

1. What is AWS Systems Manager?
2. Why Use Systems Manager?
3. Systems Manager Architecture
4. SSM Agent
5. Managed Instances
6. Session Manager
7. Run Command
8. Patch Manager
9. State Manager
10. Automation
11. Parameter Store
12. Inventory
13. Maintenance Windows
14. Fleet Manager
15. Explorer & OpsCenter
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

- Understand AWS Systems Manager (SSM)
- Manage EC2 instances without SSH
- Execute remote commands
- Store configuration securely
- Automate patching and maintenance
- Manage large fleets of servers

---

# 📖 What is AWS Systems Manager?

**AWS Systems Manager (SSM)** is a service that helps you manage, monitor, configure, and automate your AWS resources from a single place.

With Systems Manager, you can:

- 🖥️ Manage EC2 instances
- 🔐 Connect without SSH
- ⚙️ Run commands remotely
- 🔄 Patch operating systems
- 🔑 Store secrets securely
- 📊 Monitor server inventory

AWS Systems Manager reduces manual administration and improves security.

---

# 💡 Why Use Systems Manager?

Without Systems Manager:

```text
Administrator

↓

SSH into Server

↓

Run Commands

↓

Repeat for Every Server
```

Problems:

- ❌ Manual work
- ❌ SSH key management
- ❌ Difficult at scale

---

With Systems Manager:

```text
Administrator

↓

AWS Systems Manager

↓

Multiple EC2 Instances

↓

Commands Executed Automatically
```

Benefits:

- ✅ Centralized management
- ✅ No SSH required
- ✅ Secure access
- ✅ Automation
- ✅ Large-scale administration

---

# 🏗️ Systems Manager Architecture

```text
Administrator

↓

AWS Systems Manager

↓

SSM Agent

↓

EC2 Instance
```

The **SSM Agent** communicates securely with AWS Systems Manager.

---

# 🖥️ SSM Agent

The **SSM Agent** is software installed on an EC2 instance.

Responsibilities:

- Receive commands
- Execute commands
- Report results
- Send inventory
- Apply patches

Most modern Amazon Linux and Ubuntu AMIs include the SSM Agent.

---

# 📦 Managed Instances

A **Managed Instance** is any server registered with Systems Manager.

Supported resources include:

- EC2 Instances
- On-Premises Servers
- Hybrid Servers
- Edge Devices

Requirements:

- SSM Agent
- IAM Role
- Internet or VPC Endpoint connectivity

---

# 🔐 Session Manager

Session Manager lets you connect to EC2 instances securely **without SSH**.

Traditional access:

```text
Administrator

↓

SSH

↓

EC2
```

---

Using Session Manager:

```text
Administrator

↓

AWS Console / CLI

↓

Session Manager

↓

EC2
```

Benefits:

- No SSH Keys
- No Bastion Host
- Fully Logged Sessions
- Secure Access

---

# ⚙️ Run Command

Run Command executes commands on one or many instances simultaneously.

Example:

```text
Administrator

↓

Run Command

↓

100 EC2 Instances

↓

yum update
```

Example command:

```bash
sudo apt update
```

---

# 🔄 Patch Manager

Patch Manager automates operating system patching.

Supports:

- Amazon Linux
- Ubuntu
- Red Hat
- CentOS
- SUSE
- Windows

Workflow:

```text
Patch Policy

↓

Maintenance Window

↓

Automatic Updates
```

---

# 📋 State Manager

State Manager keeps servers in the desired configuration.

Example:

Ensure:

- Docker installed
- Nginx running
- CloudWatch Agent installed

Automatically reapplies configurations if they change.

---

# 🤖 Automation

Automation runs predefined workflows.

Examples:

- Restart EC2
- Create AMI
- Resize EBS Volume
- Join Active Directory
- Create Snapshots

Automation reduces repetitive tasks.

---

# 🔑 Parameter Store

Parameter Store securely stores:

- Passwords
- API Keys
- Database Credentials
- Configuration Values

Example:

```
/production/database/password
```

Supports:

- Plain Text
- SecureString (Encrypted using AWS KMS)

---

# 📊 Inventory

Inventory collects software and system information.

Example:

```
Operating System

Installed Packages

Applications

Running Services

Network Configuration
```

Useful for compliance and auditing.

---

# ⏰ Maintenance Windows

Maintenance Windows schedule administrative tasks.

Examples:

- Install updates
- Restart services
- Patch servers
- Run automation

Example:

```text
Sunday

02:00 AM

↓

Patch Servers
```

---

# 🖥️ Fleet Manager

Fleet Manager provides a graphical interface to manage EC2 instances.

Features:

- File Explorer
- Event Logs
- Performance Monitoring
- Registry Editor (Windows)
- User Management

---

# 📊 Explorer & OpsCenter

### Explorer

Provides a dashboard for:

- Compliance
- Patching
- Operational Health
- Inventory

---

### OpsCenter

Central place to investigate operational issues.

Examples:

- Failed patches
- High CPU
- Configuration drift
- System alerts

---

# 🏗️ AWS Systems Manager Architecture

```text
                 Administrator
                      │
                      ▼
            AWS Systems Manager
      ┌─────────────┬─────────────┐
      ▼             ▼             ▼
 Session Manager  Run Command  Patch Manager
      │             │             │
      └──────┬──────┴──────┬──────┘
             ▼             ▼
          SSM Agent
             │
     ┌───────┴────────┐
     ▼                ▼
  EC2-1            EC2-2
```

---

# 💻 Useful AWS CLI Commands

## List Managed Instances

```bash
aws ssm describe-instance-information
```

---

## Start a Session

```bash
aws ssm start-session \
--target i-1234567890abcdef0
```

---

## Run a Command

```bash
aws ssm send-command \
--document-name "AWS-RunShellScript" \
--targets "Key=instanceids,Values=i-1234567890abcdef0"
```

---

## List Parameters

```bash
aws ssm describe-parameters
```

---

## Get a Parameter

```bash
aws ssm get-parameter \
--name "/production/db/password" \
--with-decryption
```

---

## Put a Parameter

```bash
aws ssm put-parameter \
--name "/app/version" \
--value "1.0.0" \
--type String
```

---

# 💡 Best Practices

✅ Use Session Manager instead of SSH whenever possible.

✅ Store secrets in Parameter Store.

✅ Enable CloudTrail logging.

✅ Schedule automatic patching.

✅ Use IAM roles with least privilege.

✅ Install the latest SSM Agent.

✅ Use Maintenance Windows for updates.

✅ Monitor compliance using Explorer.

---

# 🌍 Common Use Cases

| Use Case | Systems Manager Feature |
|-----------|-------------------------|
| Remote Access | Session Manager |
| Run Linux Commands | Run Command |
| Automatic Updates | Patch Manager |
| Configuration Management | State Manager |
| Store Secrets | Parameter Store |
| Scheduled Tasks | Maintenance Windows |
| Server Inventory | Inventory |
| Troubleshooting | Fleet Manager |

---

# 📝 Key Takeaways

- Systems Manager centralizes server management.
- Session Manager removes the need for SSH.
- Run Command executes commands remotely.
- Patch Manager automates updates.
- Parameter Store securely stores secrets.
- Maintenance Windows automate administrative tasks.
- Fleet Manager provides graphical server management.

---

# 📋 Summary

In this chapter, you learned:

- AWS Systems Manager
- SSM Agent
- Managed Instances
- Session Manager
- Run Command
- Patch Manager
- State Manager
- Automation
- Parameter Store
- Inventory
- Maintenance Windows
- Fleet Manager
- Explorer
- OpsCenter
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is AWS Systems Manager?
2. What is the SSM Agent?
3. What is Session Manager?
4. What is Parameter Store?
5. What is Run Command?

---

## Intermediate

6. Explain Patch Manager.
7. What are Managed Instances?
8. What is State Manager?
9. Explain Maintenance Windows.
10. How does Systems Manager improve security?

---

## Advanced

11. Design a server management solution using Systems Manager.
12. Compare SSH and Session Manager.
13. Explain Systems Manager architecture.
14. How would you automate patch management for hundreds of EC2 instances?
15. Compare Parameter Store and AWS Secrets Manager.

---

# 🎯 Practice Exercises

## Exercise 1

Create an IAM role for Systems Manager.

---

## Exercise 2

Launch an EC2 instance with the SSM Agent installed.

---

## Exercise 3

Connect to the instance using Session Manager.

---

## Exercise 4

Use Run Command to install Nginx on multiple EC2 instances.

---

## Exercise 5

Store a database password in Parameter Store and retrieve it using the AWS CLI.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-systems-manager-guide.md
```

Include:

- Systems Manager Overview
- SSM Agent
- Session Manager
- Run Command
- Patch Manager
- State Manager
- Parameter Store
- Inventory
- Maintenance Windows
- Fleet Manager
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add AWS Systems Manager guide"
```

---

# 📚 Further Reading

- AWS Systems Manager Documentation
- SSM Agent User Guide
- AWS Parameter Store Documentation
- AWS Patch Manager Guide
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 23 – AWS IAM (Identity and Access Management)**, you'll learn:

- 👤 IAM Users
- 👥 IAM Groups
- 🎭 IAM Roles
- 📜 IAM Policies
- 🔑 Access Keys
- 🔐 Multi-Factor Authentication (MFA)
- 🌐 Cross-Account Roles
- 🛡️ Least Privilege Principle
- 💻 AWS CLI Commands
- 🚀 Hands-on IAM Labs
