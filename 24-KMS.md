# AWS Notes
# Chapter 24 - AWS Key Management Service (KMS)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is AWS KMS?
2. Why Use AWS KMS?
3. Encryption Basics
4. How AWS KMS Works
5. Customer Master Keys (KMS Keys)
6. Types of KMS Keys
7. Envelope Encryption
8. Key Policies
9. Grants
10. Key Rotation
11. AWS Service Integrations
12. Multi-Region Keys
13. CloudTrail Integration
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

- Understand AWS KMS
- Learn encryption concepts
- Create and manage KMS keys
- Encrypt and decrypt data
- Configure IAM and Key Policies
- Enable automatic key rotation
- Secure AWS resources using KMS

---

# 📖 What is AWS KMS?

**AWS Key Management Service (KMS)** is a fully managed service used to **create, manage, and control encryption keys**.

It enables you to encrypt data across AWS services without managing your own encryption infrastructure.

AWS KMS is integrated with many AWS services, including:

- 💾 Amazon S3
- 💽 Amazon EBS
- 🗄️ Amazon RDS
- 📂 Amazon EFS
- 🔐 AWS Secrets Manager
- 📦 AWS Systems Manager Parameter Store

---

# 💡 Why Use AWS KMS?

Without KMS:

```text
Application

↓

Store Plain Text Data

↓

Security Risk
```

Problems:

- ❌ Unencrypted data
- ❌ Difficult key management
- ❌ Compliance issues

---

With KMS:

```text
Application

↓

AWS KMS

↓

Encryption Key

↓

Encrypted Data
```

Benefits:

- ✅ Strong encryption
- ✅ Centralized key management
- ✅ Automatic auditing
- ✅ AWS integration

---

# 🔐 Encryption Basics

Encryption converts readable data (**Plaintext**) into unreadable data (**Ciphertext**).

Example:

```
Plaintext

↓

Encrypt

↓

Ciphertext

↓

Decrypt

↓

Plaintext
```

Only users with the correct key can decrypt the data.

---

# 🧠 How AWS KMS Works

Workflow:

```text
Application

↓

Send Data

↓

AWS KMS

↓

Encrypt

↓

Store Encrypted Data
```

When data is needed:

```text
Encrypted Data

↓

AWS KMS

↓

Decrypt

↓

Application
```

---

# 🔑 KMS Keys

A **KMS Key** is used to encrypt and decrypt data.

Each key has:

- Key ID
- ARN
- Alias
- Key Policy
- Rotation Settings

Example:

```
Alias

alias/project-key
```

---

# 🗂️ Types of KMS Keys

AWS supports several key types.

---

## AWS Owned Keys

Managed entirely by AWS.

Examples:

- Amazon S3
- DynamoDB
- CloudTrail

You cannot manage these keys.

---

## AWS Managed Keys

Created automatically for AWS services.

Example:

```
aws/s3

aws/ebs

aws/rds
```

AWS manages the key, but you can view it.

---

## Customer Managed Keys (CMK)

Created and managed by you.

Features:

- Full control
- Custom permissions
- Manual deletion
- Automatic rotation
- Cross-account sharing

Recommended for production workloads.

---

# 📦 Envelope Encryption

KMS uses **Envelope Encryption**.

Instead of encrypting large files directly:

```text
Generate Data Key

↓

Encrypt File

↓

Encrypt Data Key

↓

Store Both
```

Benefits:

- High performance
- Secure key management
- Efficient encryption

---

# 📜 Key Policies

Key Policies determine who can use a KMS key.

Example:

```json
{
  "Effect":"Allow",
  "Principal":{
      "AWS":"arn:aws:iam::123456789012:root"
  },
  "Action":"kms:*",
  "Resource":"*"
}
```

Without a Key Policy, a key cannot be accessed.

---

# 🤝 Grants

A **Grant** provides temporary permissions to use a KMS key.

Useful for:

- EC2
- Lambda
- Auto Scaling
- Temporary access

Grants are easier to manage than changing key policies.

---

# 🔄 Key Rotation

Enable automatic key rotation every year.

Benefits:

- Improved security
- Compliance
- Reduced risk

```text
Old Key

↓

Rotate

↓

New Key

↓

Existing Data Remains Accessible
```

---

# ☁️ AWS Service Integrations

AWS KMS integrates with many AWS services.

| Service | Encryption |
|----------|------------|
| Amazon S3 | ✅ |
| Amazon EBS | ✅ |
| Amazon EFS | ✅ |
| Amazon RDS | ✅ |
| DynamoDB | ✅ |
| Secrets Manager | ✅ |
| CloudTrail | ✅ |
| Systems Manager | ✅ |

---

# 🌍 Multi-Region Keys

Multi-Region Keys allow the same key to exist in multiple AWS Regions.

Benefits:

- Disaster Recovery
- Global Applications
- Simplified Encryption

Example:

```
Mumbai

↓

Replica

↓

Singapore
```

---

# 📊 CloudTrail Integration

Every KMS API call is logged by CloudTrail.

Example:

```
Encrypt

Decrypt

CreateKey

DisableKey

ScheduleKeyDeletion
```

Useful for:

- Auditing
- Security investigations
- Compliance

---

# 🏗️ AWS KMS Architecture

```text
            Application
                 │
                 ▼
             AWS KMS
        ┌────────┴────────┐
        ▼                 ▼
   Encryption Key     Key Policies
        │
        ▼
Encrypted Data Stored
 in S3 / EBS / RDS / EFS
```

---

# 💻 Useful AWS CLI Commands

## List Keys

```bash
aws kms list-keys
```

---

## Create a Key

```bash
aws kms create-key
```

---

## Create an Alias

```bash
aws kms create-alias \
--alias-name alias/project-key \
--target-key-id <key-id>
```

---

## Encrypt Data

```bash
aws kms encrypt \
--key-id alias/project-key \
--plaintext "Hello AWS"
```

---

## Decrypt Data

```bash
aws kms decrypt \
--ciphertext-blob fileb://encrypted.bin
```

---

## Describe Key

```bash
aws kms describe-key \
--key-id alias/project-key
```

---

## Enable Key Rotation

```bash
aws kms enable-key-rotation \
--key-id alias/project-key
```

---

# 💡 Best Practices

✅ Use Customer Managed Keys for production.

✅ Enable automatic key rotation.

✅ Apply the Principle of Least Privilege.

✅ Monitor KMS activity with CloudTrail.

✅ Use aliases instead of Key IDs.

✅ Never store encryption keys in applications.

✅ Delete unused keys carefully.

✅ Enable Multi-Region Keys for disaster recovery.

---

# 🌍 Common Use Cases

| Use Case | AWS KMS |
|-----------|---------|
| Encrypt S3 Buckets | ✅ |
| Encrypt EBS Volumes | ✅ |
| Encrypt RDS Databases | ✅ |
| Store Secrets | ✅ |
| Protect API Keys | ✅ |
| Encrypt Backups | ✅ |
| Secure Applications | ✅ |

---

# 📝 Key Takeaways

- AWS KMS manages encryption keys.
- Supports AWS Managed and Customer Managed Keys.
- Integrates with most AWS services.
- Uses Envelope Encryption.
- Supports automatic key rotation.
- CloudTrail records every KMS API call.
- Essential for AWS security.

---

# 📋 Summary

In this chapter, you learned:

- AWS KMS
- Encryption Basics
- KMS Keys
- Key Types
- Envelope Encryption
- Key Policies
- Grants
- Key Rotation
- Multi-Region Keys
- CloudTrail Integration
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is AWS KMS?
2. What is encryption?
3. What is a KMS Key?
4. What is the difference between plaintext and ciphertext?
5. Why do we use aliases?

---

## Intermediate

6. Explain Envelope Encryption.
7. Compare AWS Managed Keys and Customer Managed Keys.
8. What is a Key Policy?
9. What are Grants?
10. Explain Key Rotation.

---

## Advanced

11. Design a secure encryption strategy using AWS KMS.
12. Explain Multi-Region Keys.
13. How does KMS integrate with S3 and RDS?
14. Explain how CloudTrail works with KMS.
15. Compare AWS KMS with AWS CloudHSM.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Customer Managed KMS Key.

---

## Exercise 2

Create an alias for the key.

---

## Exercise 3

Enable automatic key rotation.

---

## Exercise 4

Encrypt an S3 bucket using your KMS key.

---

## Exercise 5

Review KMS API activity in CloudTrail.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-kms-guide.md
```

Include:

- AWS KMS Overview
- Encryption Basics
- KMS Key Types
- Envelope Encryption
- Key Policies
- Grants
- Key Rotation
- Multi-Region Keys
- AWS Service Integrations
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add AWS KMS guide"
```

---

# 📚 Further Reading

- AWS KMS Documentation
- AWS Encryption SDK
- AWS Security Best Practices
- AWS CloudTrail Documentation
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 25 – AWS IAM (Identity and Access Management)**, you'll learn:

- 👤 IAM Users
- 👥 IAM Groups
- 🎭 IAM Roles
- 📜 IAM Policies
- 🔑 Access Keys
- 🔐 Multi-Factor Authentication (MFA)
- 🌐 Cross-Account Access
- 🛡️ IAM Security Best Practices
- 💻 AWS CLI Commands
- 🚀 Hands-on IAM Labs
