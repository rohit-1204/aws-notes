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
4. Symmetric vs Asymmetric Keys
5. How AWS KMS Works
6. Types of KMS Keys
7. Envelope Encryption
8. Key Policies
9. Grants
10. Key Rotation
11. Multi-Region Keys
12. AWS Service Integrations
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

- Understand AWS Key Management Service (KMS)
- Learn encryption fundamentals
- Create and manage KMS keys
- Encrypt and decrypt data
- Configure key policies and IAM permissions
- Enable automatic key rotation
- Secure AWS resources using KMS

---

# 📖 What is AWS KMS?

**AWS Key Management Service (AWS KMS)** is a fully managed encryption service that lets you create, manage, and control cryptographic keys.

Instead of managing encryption keys yourself, AWS securely stores and manages them.

AWS KMS integrates with many AWS services for encrypting data.

---

# 💡 Why Use AWS KMS?

Without KMS:

```text
Application

↓

Store Plain Data

↓

Security Risk
```

Problems:

- ❌ Plain-text data
- ❌ Manual key management
- ❌ Difficult compliance

---

With AWS KMS:

```text
Application

↓

AWS KMS

↓

Encrypt Data

↓

Store Securely
```

Benefits:

- ✅ Secure encryption
- ✅ Centralized key management
- ✅ Automatic auditing
- ✅ IAM integration
- ✅ Compliance support

---

# 🔐 Encryption Basics

Encryption converts readable data (**Plaintext**) into unreadable data (**Ciphertext**).

```text
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

Only authorized users with the correct key can decrypt the data.

---

# 🔑 Symmetric vs Asymmetric Keys

## Symmetric Keys

Uses the **same key** for encryption and decryption.

```text
Encrypt

↓

Shared Key

↓

Decrypt
```

Advantages:

- Fast
- Efficient
- Used by most AWS services

---

## Asymmetric Keys

Uses two keys:

- Public Key
- Private Key

```text
Public Key

↓

Encrypt

↓

Private Key

↓

Decrypt
```

Commonly used for:

- Digital Signatures
- Secure Communication

---

# ⚙️ How AWS KMS Works

Workflow:

```text
Application

↓

Request Encryption

↓

AWS KMS

↓

Encrypt Data

↓

Encrypted Data Stored
```

When reading:

```text
Encrypted Data

↓

AWS KMS

↓

Decrypt

↓

Application
```

AWS never exposes the encryption key.

---

# 🔑 Types of KMS Keys

## AWS Owned Keys

Created and managed entirely by AWS.

Examples:

- Amazon S3
- DynamoDB
- CloudTrail

---

## AWS Managed Keys

Automatically created for AWS services.

Examples:

```
aws/s3

aws/ebs

aws/rds
```

You can view them but cannot fully manage them.

---

## Customer Managed Keys (CMKs)

Created and managed by you.

Advantages:

- Custom permissions
- Key rotation
- Aliases
- Cross-account sharing
- Full lifecycle control

Recommended for production workloads.

---

# 📦 Envelope Encryption

AWS KMS uses **Envelope Encryption** for large data.

Instead of encrypting files directly:

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
- Faster encryption

---

# 📜 Key Policies

Every KMS key has a **Key Policy**.

Key Policies determine who can:

- Encrypt
- Decrypt
- Rotate
- Delete
- Manage the key

Example:

```json
{
  "Effect": "Allow",
  "Action": "kms:*",
  "Resource": "*"
}
```

---

# 🤝 Grants

A **Grant** gives temporary permission to use a KMS key.

Used by services like:

- EC2
- Lambda
- Auto Scaling
- ECS

Benefits:

- Temporary access
- No policy modification
- Easier delegation

---

# 🔄 Key Rotation

Automatic key rotation generates a new cryptographic key every year.

```text
Old Key

↓

Rotate

↓

New Key
```

Benefits:

- Better security
- Compliance
- Reduced key exposure

Existing encrypted data remains accessible.

---

# 🌍 Multi-Region Keys

Multi-Region Keys allow the same key to exist across AWS Regions.

Example:

```text
Mumbai

↓

Replica

↓

Singapore
```

Benefits:

- Disaster Recovery
- Global Applications
- Consistent encryption

---

# ☁️ AWS Services Integrated with KMS

| AWS Service | Supports KMS |
|-------------|--------------|
| Amazon S3 | ✅ |
| Amazon EBS | ✅ |
| Amazon EFS | ✅ |
| Amazon RDS | ✅ |
| DynamoDB | ✅ |
| Secrets Manager | ✅ |
| Systems Manager | ✅ |
| CloudTrail | ✅ |
| Lambda | ✅ |

---

# 📊 CloudTrail Integration

Every KMS API request is recorded by CloudTrail.

Examples:

- CreateKey
- Encrypt
- Decrypt
- DisableKey
- ScheduleKeyDeletion

Useful for:

- Auditing
- Compliance
- Security investigations

---

# 🏗️ AWS KMS Architecture

```text
             Application
                  │
                  ▼
             AWS KMS
        ┌─────────┴─────────┐
        ▼                   ▼
 Encryption Keys      Key Policies
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

## Enable Automatic Rotation

```bash
aws kms enable-key-rotation \
--key-id alias/project-key
```

---

# 💡 Best Practices

✅ Use Customer Managed Keys for production.

✅ Enable automatic key rotation.

✅ Follow the Principle of Least Privilege.

✅ Use aliases instead of Key IDs.

✅ Monitor KMS usage using CloudTrail.

✅ Restrict access using IAM and Key Policies.

✅ Delete unused keys carefully.

✅ Use Multi-Region Keys for DR workloads.

---

# 🌍 Common Use Cases

| Scenario | KMS |
|-----------|-----|
| Encrypt S3 Buckets | ✅ |
| Encrypt EBS Volumes | ✅ |
| Encrypt RDS | ✅ |
| Secure Secrets | ✅ |
| Protect API Keys | ✅ |
| Encrypt Backups | ✅ |
| Compliance | ✅ |

---

# 📝 Key Takeaways

- AWS KMS manages encryption keys.
- Supports symmetric and asymmetric keys.
- Uses Envelope Encryption.
- Integrates with most AWS services.
- Supports automatic key rotation.
- CloudTrail logs all KMS API activity.
- Essential for securing cloud workloads.

---

# 📋 Summary

In this chapter, you learned:

- AWS KMS
- Encryption Basics
- Symmetric & Asymmetric Keys
- KMS Key Types
- Envelope Encryption
- Key Policies
- Grants
- Key Rotation
- Multi-Region Keys
- AWS Service Integration
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
5. Why do we use KMS?

---

## Intermediate

6. Explain Envelope Encryption.
7. Compare AWS Managed Keys and Customer Managed Keys.
8. What is a Key Policy?
9. What are Grants?
10. Explain automatic key rotation.

---

## Advanced

11. Design a secure encryption strategy using AWS KMS.
12. Explain Multi-Region Keys.
13. How does KMS integrate with Amazon S3?
14. Explain CloudTrail integration with KMS.
15. Compare AWS KMS and AWS CloudHSM.

---

# 🎯 Practice Exercises

## Exercise 1

Create a Customer Managed Key.

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

Review KMS API events in CloudTrail.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-kms-guide.md
```

Include:

- AWS KMS Overview
- Encryption Concepts
- KMS Key Types
- Envelope Encryption
- Key Policies
- Key Rotation
- Multi-Region Keys
- AWS Integrations
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

In **Chapter 25 – AWS Lambda**, you'll learn:

- ⚡ Serverless Computing
- 🚀 Lambda Functions
- 📦 Deployment Packages
- 🌐 Event Sources
- 🔄 Function Triggers
- 📊 Monitoring with CloudWatch
- 🔐 IAM Roles
- 💻 AWS CLI Commands
- 🛠️ Hands-on Serverless Projects
