# AWS Notes
# Chapter 36 - AWS Security Best Practices

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. Introduction
2. AWS Shared Responsibility Model
3. Identity and Access Management (IAM)
4. Multi-Factor Authentication (MFA)
5. Least Privilege Principle
6. Password Policies
7. AWS Organizations
8. Network Security
9. Security Groups & NACLs
10. Encryption
11. Secrets Management
12. Logging & Auditing
13. Monitoring & Threat Detection
14. Backup & Disaster Recovery
15. Compliance
16. Security Best Practices
17. Summary
18. Interview Questions
19. Practice Exercises
20. Mini Project
21. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand AWS security fundamentals
- Apply IAM best practices
- Secure AWS resources
- Protect sensitive data
- Monitor security events
- Build secure cloud environments

---

# 📖 Introduction

Security is one of the most important aspects of AWS.

AWS provides secure infrastructure, while customers are responsible for securing their applications, data, and configurations.

A secure AWS environment reduces the risk of:

- Unauthorized access
- Data breaches
- Service disruptions
- Compliance violations

---

# 🛡️ AWS Shared Responsibility Model

AWS security responsibilities are divided between AWS and the customer.

```text
           AWS
----------------------------
✔ Data Centers
✔ Physical Security
✔ Hardware
✔ Networking
✔ Global Infrastructure

----------------------------

         Customer
----------------------------
✔ IAM Users
✔ Applications
✔ Data
✔ Operating System
✔ Network Configuration
✔ Encryption
```

Remember:

> AWS secures **the cloud**.  
> You secure **what you put in the cloud**.

---

# 👤 Identity and Access Management (IAM)

IAM controls who can access AWS resources.

Main components:

- Users
- Groups
- Roles
- Policies

Benefits:

- Secure authentication
- Fine-grained permissions
- Centralized access management

---

# 🔐 Multi-Factor Authentication (MFA)

MFA requires users to provide:

- Password
- Verification Code

Benefits:

- Extra security
- Protects root account
- Prevents unauthorized access

Always enable MFA for:

- Root User
- Administrator Accounts

---

# 🎯 Principle of Least Privilege

Users should receive **only the permissions required** to perform their tasks.

Example:

```text
Developer

↓

Access to EC2

❌ No access to Billing

❌ No access to IAM
```

Benefits:

- Reduced attack surface
- Better security
- Easier auditing

---

# 🔑 Password Policies

Strong password policies improve account security.

Recommendations:

- Minimum 12 characters
- Uppercase letters
- Lowercase letters
- Numbers
- Special characters
- Password rotation (if required)

---

# 🏢 AWS Organizations

AWS Organizations helps manage multiple AWS accounts.

Features:

- Centralized management
- Service Control Policies (SCPs)
- Consolidated billing
- Organizational Units (OUs)

Ideal for enterprise environments.

---

# 🌐 Network Security

Protect your network using:

- Amazon VPC
- Private Subnets
- Security Groups
- Network ACLs
- NAT Gateway
- VPN
- AWS Direct Connect

Avoid exposing unnecessary resources to the internet.

---

# 🔥 Security Groups & NACLs

### Security Groups

- Instance-level firewall
- Stateful
- Allow rules only

### Network ACLs

- Subnet-level firewall
- Stateless
- Allow and Deny rules

Use both together for layered security.

---

# 🔒 Encryption

Encrypt data:

- At Rest
- In Transit

AWS services:

- AWS KMS
- AWS Certificate Manager (ACM)
- SSL/TLS
- HTTPS

Encrypt:

- S3 Buckets
- EBS Volumes
- RDS Databases
- EFS File Systems

---

# 🔑 Secrets Management

Never hardcode:

- Passwords
- API Keys
- Database Credentials

Use:

- AWS Secrets Manager
- AWS Systems Manager Parameter Store

Benefits:

- Automatic rotation
- Secure storage
- IAM integration

---

# 📜 Logging & Auditing

Enable logging using:

- AWS CloudTrail
- CloudWatch Logs
- VPC Flow Logs
- S3 Access Logs

Benefits:

- Compliance
- Troubleshooting
- Security investigations

---

# 🚨 Monitoring & Threat Detection

AWS security services:

- Amazon CloudWatch
- AWS GuardDuty
- AWS Security Hub
- Amazon Inspector
- AWS Config

Monitor:

- Unauthorized access
- Configuration changes
- Vulnerabilities
- Suspicious activity

---

# 💾 Backup & Disaster Recovery

Always back up critical resources.

Examples:

- Amazon EBS Snapshots
- Amazon RDS Backups
- Amazon S3 Versioning
- AWS Backup

Follow the **3-2-1 Backup Rule**:

- 3 Copies
- 2 Different Storage Types
- 1 Offsite Copy

---

# 📋 Compliance

AWS supports many compliance standards:

- ISO 27001
- SOC
- PCI DSS
- HIPAA
- GDPR

Use AWS Artifact to access compliance reports.

---

# 🏗️ Secure AWS Architecture

```text
Users
   │
   ▼
IAM + MFA
   │
   ▼
Amazon VPC
   │
 ┌─┴────────────┐
 ▼              ▼
Private      Public
Subnet       Subnet
 │              │
 ▼              ▼
EC2          Load Balancer
 │
 ▼
Encrypted Database
 │
 ▼
CloudWatch + CloudTrail
```

---

# 🏆 AWS Security Best Practices

- ✅ Enable MFA
- ✅ Follow Least Privilege
- ✅ Avoid using Root User
- ✅ Rotate credentials regularly
- ✅ Encrypt sensitive data
- ✅ Store secrets securely
- ✅ Enable CloudTrail
- ✅ Monitor using CloudWatch
- ✅ Keep software updated
- ✅ Perform regular backups
- ✅ Restrict inbound network access
- ✅ Review IAM policies regularly

---

# 🌍 Common Use Cases

| Scenario | AWS Service |
|----------|-------------|
| Identity Management | IAM |
| Encryption | KMS |
| Secret Storage | Secrets Manager |
| Monitoring | CloudWatch |
| Auditing | CloudTrail |
| Threat Detection | GuardDuty |
| Vulnerability Assessment | Inspector |
| Backup | AWS Backup |

---

# 📝 Key Takeaways

- Security is a shared responsibility.
- Always use IAM and MFA.
- Follow the Principle of Least Privilege.
- Encrypt sensitive data.
- Monitor with CloudWatch and CloudTrail.
- Store secrets securely.
- Enable backups and logging.

---

# 📋 Summary

In this chapter, you learned:

- Shared Responsibility Model
- IAM
- MFA
- Least Privilege
- Password Policies
- AWS Organizations
- Network Security
- Encryption
- Secrets Management
- Logging
- Monitoring
- Compliance
- Backup
- Security Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is the AWS Shared Responsibility Model?
2. Why should MFA be enabled?
3. What is IAM?
4. What is the Principle of Least Privilege?
5. Why is encryption important?

---

## Intermediate

6. Compare Security Groups and Network ACLs.
7. Explain AWS Secrets Manager.
8. What is AWS GuardDuty?
9. Explain CloudTrail's role in security.
10. Why should the Root User not be used daily?

---

## Advanced

11. Design a secure AWS architecture.
12. Explain defense-in-depth in AWS.
13. How would you secure production workloads?
14. Compare KMS and Secrets Manager.
15. Explain AWS security best practices for DevOps.

---

# 🎯 Practice Exercises

## Exercise 1

Enable MFA for your AWS account.

---

## Exercise 2

Create an IAM Role with least privilege permissions.

---

## Exercise 3

Encrypt an S3 bucket using AWS KMS.

---

## Exercise 4

Store a database password in AWS Secrets Manager.

---

## Exercise 5

Enable CloudTrail and review API activity.

---

# 🧩 Mini Project

Secure a sample AWS application.

Tasks:

- Create IAM users and roles
- Enable MFA
- Configure Security Groups
- Encrypt storage with KMS
- Store secrets securely
- Enable CloudTrail
- Configure CloudWatch alarms
- Review security logs

Commit your project:

```bash
git add .
git commit -m "Implement AWS security best practices"
```

---

# 📚 Further Reading

- AWS Security Best Practices Guide
- AWS IAM Documentation
- AWS KMS Documentation
- AWS GuardDuty Documentation
- AWS Well-Architected Security Pillar

---

# 🚀 What's Next?

In **Chapter 37 – AWS Cost Optimization**, you'll learn:

- 💰 AWS Pricing Models
- 📊 Cost Explorer
- 🖥️ EC2 Cost Optimization
- 💾 Storage Optimization
- 📈 Reserved Instances
- ⚡ Savings Plans
- 📋 AWS Budgets
- 🛠️ Cost Optimization Best Practices
