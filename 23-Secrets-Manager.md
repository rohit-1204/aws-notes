# AWS Notes
# Chapter 23 - AWS Secrets Manager

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is AWS Secrets Manager?
2. Why Use Secrets Manager?
3. Secrets Manager vs Parameter Store
4. How Secrets Manager Works
5. Secret Rotation
6. AWS KMS Integration
7. Secret Versions
8. Access Control with IAM
9. Monitoring & Auditing
10. Architecture
11. AWS CLI Commands
12. Best Practices
13. Common Use Cases
14. Summary
15. Interview Questions
16. Practice Exercises
17. Mini Project
18. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand AWS Secrets Manager
- Store sensitive credentials securely
- Automatically rotate secrets
- Integrate Secrets Manager with applications
- Control access using IAM
- Audit secret access

---

# 📖 What is AWS Secrets Manager?

**AWS Secrets Manager** is a fully managed service for securely storing, managing, and rotating sensitive information.

Examples of secrets include:

- 🔑 Database Passwords
- 🔐 API Keys
- 🔒 SSH Keys
- 🌐 OAuth Tokens
- ☁️ AWS Credentials
- 🔑 Third-party Service Credentials

Secrets are encrypted using **AWS Key Management Service (KMS)**.

---

# 💡 Why Use Secrets Manager?

Without Secrets Manager:

```text
Developer

↓

Password in Source Code

↓

Git Repository

↓

Security Risk
```

Problems:

- ❌ Hardcoded credentials
- ❌ Difficult rotation
- ❌ High security risk

---

With Secrets Manager:

```text
Application

↓

Secrets Manager

↓

Encrypted Secret

↓

AWS KMS
```

Benefits:

- ✅ Secure storage
- ✅ Automatic rotation
- ✅ Centralized management
- ✅ Audit logging

---

# ⚖️ Secrets Manager vs Parameter Store

| Feature | Secrets Manager | Parameter Store |
|----------|-----------------|----------------|
| Secret Storage | ✅ | ✅ |
| Automatic Rotation | ✅ | ❌ |
| AWS KMS Encryption | ✅ | ✅ |
| Versioning | ✅ | Limited |
| Database Credential Rotation | ✅ | ❌ |
| Cost | Paid | Free (Standard Tier) |

---

# 🧠 How Secrets Manager Works

Workflow:

```text
Application

↓

Request Secret

↓

AWS Secrets Manager

↓

Decrypt using AWS KMS

↓

Return Secret
```

Applications retrieve secrets dynamically instead of storing them in code.

---

# 🔄 Secret Rotation

Secrets Manager can automatically rotate secrets.

Supported services include:

- Amazon RDS
- Amazon Aurora
- Redshift
- Custom Databases

Example:

```text
Old Password

↓

Rotate Automatically

↓

New Password

↓

Application Updated
```

Rotation is typically performed using **AWS Lambda**.

---

# 🔐 AWS KMS Integration

Secrets are encrypted using AWS KMS.

```text
Secret

↓

AWS KMS

↓

Encrypted Secret

↓

Stored Securely
```

Benefits:

- Encryption at Rest
- Controlled Key Access
- Compliance Support

---

# 📂 Secret Versions

Every time a secret is updated, a new version is created.

Example:

```text
Version 1

↓

Version 2

↓

Version 3
```

Version labels include:

- AWSCURRENT
- AWSPREVIOUS
- AWSPENDING

---

# 👤 IAM Access Control

Access to secrets is controlled using IAM.

Example Policy:

```json
{
  "Effect": "Allow",
  "Action": [
    "secretsmanager:GetSecretValue"
  ],
  "Resource": "*"
}
```

Follow the **Principle of Least Privilege**.

---

# 📊 Monitoring & Auditing

Secrets Manager integrates with:

- 📜 AWS CloudTrail
- 📈 Amazon CloudWatch
- 🔔 Amazon EventBridge

Track:

- Secret creation
- Secret retrieval
- Secret updates
- Rotation events

---

# 🏗️ AWS Secrets Manager Architecture

```text
             Application
                  │
                  ▼
       AWS Secrets Manager
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
   AWS KMS Encryption   Secret Versions
                  │
                  ▼
          Database / API
```

---

# 💻 Useful AWS CLI Commands

## Create a Secret

```bash
aws secretsmanager create-secret \
--name MyDatabasePassword \
--secret-string "MySecurePassword123"
```

---

## List Secrets

```bash
aws secretsmanager list-secrets
```

---

## Retrieve a Secret

```bash
aws secretsmanager get-secret-value \
--secret-id MyDatabasePassword
```

---

## Update a Secret

```bash
aws secretsmanager update-secret \
--secret-id MyDatabasePassword \
--secret-string "NewPassword123"
```

---

## Delete a Secret

```bash
aws secretsmanager delete-secret \
--secret-id MyDatabasePassword
```

---

# 💡 Best Practices

✅ Never hardcode secrets in applications.

✅ Enable automatic secret rotation.

✅ Encrypt all secrets using AWS KMS.

✅ Restrict access with IAM policies.

✅ Monitor access using CloudTrail.

✅ Use meaningful secret names.

✅ Rotate database passwords regularly.

✅ Delete unused secrets.

---

# 🌍 Common Use Cases

| Scenario | Secrets Manager |
|----------|-----------------|
| Database Passwords | ✅ |
| API Keys | ✅ |
| OAuth Tokens | ✅ |
| SSH Credentials | ✅ |
| Kubernetes Secrets | ✅ |
| Third-party Credentials | ✅ |
| Application Configuration | ✅ |

---

# 📝 Key Takeaways

- Secrets Manager securely stores sensitive data.
- Supports automatic secret rotation.
- Integrates with AWS KMS for encryption.
- Provides version management.
- Works with CloudTrail for auditing.
- Ideal for production applications.

---

# 📋 Summary

In this chapter, you learned:

- AWS Secrets Manager
- Secret Storage
- Secret Rotation
- AWS KMS Integration
- Secret Versions
- IAM Access Control
- Monitoring
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is AWS Secrets Manager?
2. Why should secrets not be stored in source code?
3. What is secret rotation?
4. Which AWS service encrypts secrets?
5. Can Secrets Manager store API keys?

---

## Intermediate

6. Compare Secrets Manager and Parameter Store.
7. How does automatic rotation work?
8. Explain secret versioning.
9. How is IAM used with Secrets Manager?
10. How can you audit secret access?

---

## Advanced

11. Design a secure credential management solution using Secrets Manager.
12. Explain the integration between Secrets Manager and AWS Lambda.
13. How would you rotate database credentials automatically?
14. Compare Secrets Manager with HashiCorp Vault.
15. How does Secrets Manager improve application security?

---

# 🎯 Practice Exercises

## Exercise 1

Create a secret containing a database password.

---

## Exercise 2

Retrieve the secret using the AWS CLI.

---

## Exercise 3

Update the secret value.

---

## Exercise 4

Create an IAM policy allowing read-only access to secrets.

---

## Exercise 5

Enable automatic rotation for an RDS database credential.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-secrets-manager-guide.md
```

Include:

- Secrets Manager Overview
- Secret Rotation
- AWS KMS
- Secret Versions
- IAM Access Control
- Monitoring
- AWS CLI Commands
- Best Practices
- Secrets Manager vs Parameter Store

Commit it to Git:

```bash
git add .
git commit -m "Add AWS Secrets Manager guide"
```

---

# 📚 Further Reading

- AWS Secrets Manager Documentation
- AWS KMS Documentation
- AWS IAM Documentation
- AWS Security Best Practices
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 24 – AWS IAM (Identity and Access Management)**, you'll learn:

- 👤 IAM Users
- 👥 IAM Groups
- 🎭 IAM Roles
- 📜 IAM Policies
- 🔑 Access Keys
- 🔐 Multi-Factor Authentication (MFA)
- 🌐 Cross-Account Roles
- 🛡️ IAM Best Practices
- 💻 AWS CLI Commands
- 🚀 Hands-on IAM Labs
