# AWS Notes
# Chapter 19 - Amazon EFS (Elastic File System)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is Amazon EFS?
2. Why Use EFS?
3. EFS vs EBS vs S3
4. How Amazon EFS Works
5. EFS Architecture
6. Performance Modes
7. Throughput Modes
8. Storage Classes
9. Mount Targets
10. Security
11. Backup & Recovery
12. AWS CLI Commands
13. Best Practices
14. Common Use Cases
15. Summary
16. Interview Questions
17. Practice Exercises
18. Mini Project
19. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon EFS
- Differentiate EFS, EBS and S3
- Mount EFS on EC2 instances
- Configure security and access
- Understand storage classes and performance modes
- Build shared storage for applications

---

# 📖 What is Amazon EFS?

**Amazon Elastic File System (EFS)** is a fully managed **Network File System (NFS)** that provides scalable shared file storage for Linux-based workloads.

Unlike Amazon EBS, one EFS file system can be mounted on **multiple EC2 instances simultaneously**.

AWS automatically manages:

- 📈 Storage scaling
- 💾 Data durability
- 🔄 Availability
- 🛡️ Redundancy
- ⚙️ Maintenance

---

# 💡 Why Use EFS?

Suppose you have multiple web servers.

Without EFS:

```text
EC2-1 → Own Storage

EC2-2 → Own Storage

EC2-3 → Own Storage
```

Files are different on every server.

---

With EFS:

```text
        Amazon EFS
      ┌─────────────┐
      │ Shared Data │
      └─────────────┘
      ▲      ▲      ▲
      │      │      │
    EC2-1  EC2-2  EC2-3
```

All servers share the same files.

---

# ⚖️ Amazon EFS vs EBS vs S3

| Feature | Amazon EFS | Amazon EBS | Amazon S3 |
|----------|------------|------------|-----------|
| Storage Type | File | Block | Object |
| Multiple EC2 Access | ✅ Yes | ❌ No | Via API |
| Automatically Scales | ✅ | ❌ | ✅ |
| Linux File System | ✅ | ✅ | ❌ |
| Suitable for Shared Storage | ✅ | ❌ | ❌ |

---

# 🧠 How Amazon EFS Works

Amazon EFS uses the **NFS (Network File System)** protocol.

Workflow:

```text
EC2 Instance

↓

NFS Client

↓

Amazon EFS

↓

Shared Files
```

Applications can read and write files just like a local file system.

---

# 🏗️ Amazon EFS Architecture

```text
                  Amazon VPC
                      │
        ┌─────────────┴─────────────┐
        ▼                           ▼
 Availability Zone A         Availability Zone B
        │                           │
   Mount Target A             Mount Target B
        │                           │
        ▼                           ▼
      EC2-1                      EC2-2
             \                 /
              \               /
               ─── Amazon EFS ───
```

Each Availability Zone contains a **Mount Target** for low-latency access.

---

# 📂 File System

An EFS File System behaves like a Linux directory.

Example:

```
/
├── uploads
├── images
├── logs
├── backup
└── shared
```

Every connected EC2 instance sees the same directory structure.

---

# 📍 Mount Targets

A **Mount Target** provides an endpoint inside a subnet.

Each Availability Zone should have its own mount target.

Benefits:

- Lower latency
- High availability
- Better performance

---

# 🚀 Performance Modes

Amazon EFS provides two performance modes.

---

## General Purpose

Best for:

- Web applications
- CMS
- Development
- Home directories

Features:

- Low latency
- Recommended for most workloads

---

## Max I/O

Designed for:

- Big data
- Media processing
- High parallel workloads

Features:

- Higher throughput
- Slightly higher latency

---

# ⚡ Throughput Modes

---

## Bursting Throughput

Default mode.

Performance increases automatically as storage grows.

Suitable for:

- Small and medium workloads

---

## Provisioned Throughput

You define the throughput manually.

Useful when:

- Storage is small
- Performance requirements are high

---

## Elastic Throughput

Automatically adjusts throughput based on workload.

Best for unpredictable traffic.

---

# 💾 Storage Classes

Amazon EFS supports multiple storage classes.

| Storage Class | Purpose |
|---------------|----------|
| Standard | Frequently accessed files |
| Infrequent Access (IA) | Rarely accessed files |
| Archive | Long-term storage |

Lifecycle policies automatically move files between storage classes.

---

# 🔐 Security

Amazon EFS supports:

- Security Groups
- IAM Policies
- Encryption at Rest
- Encryption in Transit
- AWS KMS
- POSIX File Permissions

---

# 🔒 Access Points

EFS Access Points simplify access management.

Benefits:

- Application-specific access
- Different root directories
- Separate permissions
- Easier administration

Example:

```text
Application A

↓

/app1

--------------------

Application B

↓

/app2
```

---

# 💾 Backup & Recovery

Amazon EFS integrates with:

- AWS Backup
- Snapshots
- Cross-Region Backup

Benefits:

- Disaster Recovery
- Automatic Backups
- Data Protection

---

# ❤️ High Availability

Amazon EFS automatically stores data across multiple Availability Zones.

```text
Write File

↓

Availability Zone A

↓

Replicated

↓

Availability Zone B
```

If one AZ fails, data remains available.

---

# 💻 Mounting EFS on Linux

Install NFS client:

```bash
sudo apt install nfs-common
```

---

Create mount directory:

```bash
sudo mkdir /mnt/efs
```

---

Mount EFS:

```bash
sudo mount -t nfs4 \
fs-12345678.efs.ap-south-1.amazonaws.com:/ /mnt/efs
```

---

Verify:

```bash
df -h
```

---

# 💻 Useful AWS CLI Commands

## Create File System

```bash
aws efs create-file-system
```

---

## List File Systems

```bash
aws efs describe-file-systems
```

---

## Create Mount Target

```bash
aws efs create-mount-target \
--file-system-id fs-12345678 \
--subnet-id subnet-xxxx \
--security-groups sg-xxxx
```

---

## Describe Mount Targets

```bash
aws efs describe-mount-targets \
--file-system-id fs-12345678
```

---

## Delete File System

```bash
aws efs delete-file-system \
--file-system-id fs-12345678
```

---

# 💡 Best Practices

✅ Use one Mount Target per Availability Zone.

✅ Enable encryption at rest.

✅ Enable encryption in transit.

✅ Use Lifecycle Management.

✅ Use Access Points for applications.

✅ Monitor with CloudWatch.

✅ Restrict access using Security Groups.

✅ Take regular backups.

---

# 🌍 Common Use Cases

| Application | Use EFS |
|--------------|---------|
| WordPress | ✅ |
| Shared Website Content | ✅ |
| CMS | ✅ |
| Machine Learning | ✅ |
| Container Storage | ✅ |
| Home Directories | ✅ |
| Shared Application Files | ✅ |

---

# 📝 Key Takeaways

- Amazon EFS is a managed network file system.
- Supports multiple EC2 instances simultaneously.
- Uses the NFS protocol.
- Automatically scales storage.
- Supports lifecycle management.
- Highly available across Availability Zones.
- Ideal for shared Linux file systems.

---

# 📋 Summary

In this chapter, you learned:

- Amazon EFS
- File Systems
- Mount Targets
- Performance Modes
- Throughput Modes
- Storage Classes
- Access Points
- Security
- Backup & Recovery
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Amazon EFS?
2. How is EFS different from EBS?
3. Which protocol does EFS use?
4. What is a Mount Target?
5. Can multiple EC2 instances use one EFS?

---

## Intermediate

6. Explain Performance Modes.
7. What are Throughput Modes?
8. What are Access Points?
9. Explain Lifecycle Management.
10. How is EFS highly available?

---

## Advanced

11. Design a highly available shared storage solution using EFS.
12. Compare Amazon EFS, Amazon EBS and Amazon S3.
13. Explain how EFS integrates with Auto Scaling.
14. How would you secure an EFS file system?
15. Explain EFS architecture across multiple Availability Zones.

---

# 🎯 Practice Exercises

## Exercise 1

Create an Amazon EFS file system.

---

## Exercise 2

Create Mount Targets in two Availability Zones.

---

## Exercise 3

Mount the EFS file system on two EC2 instances.

---

## Exercise 4

Create a file on EC2-1 and verify it appears on EC2-2.

---

## Exercise 5

Enable Lifecycle Management and observe file movement to the IA storage class.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-efs-guide.md
```

Include:

- Amazon EFS Overview
- Architecture
- Mount Targets
- Performance Modes
- Throughput Modes
- Storage Classes
- Access Points
- Security
- Backup
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Amazon EFS guide"
```

---

# 📚 Further Reading

- Amazon EFS Documentation
- Amazon EFS User Guide
- AWS Backup Documentation
- Amazon EFS Performance Guide
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 20 – AWS IAM (Identity and Access Management)**, you'll learn:

- 👤 IAM Users
- 👥 IAM Groups
- 🎭 IAM Roles
- 📜 IAM Policies
- 🔑 Access Keys
- 🔐 Multi-Factor Authentication (MFA)
- 🌐 Cross-Account Access
- 🛡️ IAM Best Practices
- 💻 AWS CLI Commands
- 🚀 Hands-on Labs
