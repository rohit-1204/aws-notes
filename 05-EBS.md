# AWS Notes
# Chapter 05 - Amazon EBS (Elastic Block Store)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is Amazon EBS?
2. Why Use EBS?
3. EBS Architecture
4. EBS Volume Types
5. EBS vs Instance Store
6. Creating an EBS Volume
7. Attaching an EBS Volume
8. Mounting an EBS Volume (Linux)
9. Resizing an EBS Volume
10. EBS Snapshots
11. EBS Encryption
12. EBS Performance
13. Monitoring EBS
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

- Understand Amazon EBS
- Differentiate EBS and Instance Store
- Create and attach EBS volumes
- Format and mount EBS volumes
- Create and restore snapshots
- Encrypt EBS volumes
- Monitor storage performance
- Manage EBS using AWS CLI

---

# 📖 What is Amazon EBS?

**Amazon Elastic Block Store (EBS)** is a persistent block storage service designed for Amazon EC2 instances.

Think of an EBS volume as a **virtual hard disk (SSD/HDD)** attached to an EC2 instance.

Unlike the root disk of many traditional virtual machines, EBS volumes can be detached and attached to another compatible EC2 instance.

---

# 💡 Why Use Amazon EBS?

Amazon EBS provides:

- 💾 Persistent Storage
- ⚡ High Performance SSD
- 📸 Snapshots
- 🔐 Encryption
- 📈 Easy Scaling
- 🔄 Backup & Recovery
- 🛡️ High Availability

---

# 🏗️ Amazon EBS Architecture

```text
                EC2 Instance
                     │
        ┌────────────┴────────────┐
        │                         │
        ▼                         ▼
   Root EBS Volume         Additional EBS Volume
        │                         │
        └────────────┬────────────┘
                     ▼
              Amazon EBS Storage
                     │
                     ▼
               EBS Snapshots (S3)
```

---

# 🧠 Understanding Block Storage

Block storage divides data into fixed-size blocks.

Each block has its own address and can be read or written independently.

Examples of block storage:

- Amazon EBS
- Local SSD
- SAN Storage

Block storage is ideal for:

- Operating Systems
- Databases
- Virtual Machines
- Enterprise Applications

---

# 📦 EBS Volume Types

AWS provides multiple EBS volume types.

| Volume Type | Category | Best For |
|-------------|-----------|----------|
| gp3 | SSD | General workloads |
| gp2 | SSD | Legacy general-purpose workloads |
| io2 | SSD | High-performance databases |
| io1 | SSD | Provisioned IOPS (older generation) |
| st1 | HDD | Frequently accessed HDD workloads |
| sc1 | HDD | Infrequently accessed data |

---

# ⚡ gp3 (General Purpose SSD)

Recommended for most workloads.

Suitable for:

- Linux servers
- Windows servers
- Web applications
- Development environments

Benefits:

- High performance
- Independent IOPS configuration
- Cost-effective

---

# 🚀 io2 (Provisioned IOPS SSD)

Designed for mission-critical applications.

Examples:

- Oracle Database
- Microsoft SQL Server
- SAP HANA

Provides:

- Extremely high IOPS
- Low latency
- High durability

---

# 💽 st1 (Throughput Optimized HDD)

Ideal for:

- Big Data
- Data Warehousing
- Log Processing
- Streaming Workloads

---

# 🗄️ sc1 (Cold HDD)

Designed for:

- Backup
- Archives
- Cold Storage
- Infrequently accessed data

---

# ⚖️ EBS vs Instance Store

| Amazon EBS | Instance Store |
|-------------|----------------|
| Persistent | Temporary |
| Network Attached | Physically Attached |
| Supports Snapshots | No Snapshots |
| Can be Detached | Cannot be Detached |
| Supports Encryption | Limited |
| Recommended for Production | Temporary Cache Only |

---

# 📀 Creating an EBS Volume

Steps:

1. Open the EC2 Console.
2. Navigate to **Elastic Block Store → Volumes**.
3. Click **Create Volume**.
4. Select:
   - Volume Type
   - Size
   - Availability Zone
5. Click **Create Volume**.

> ⚠️ An EBS volume must be in the **same Availability Zone** as the EC2 instance.

---

# 🔗 Attaching an EBS Volume

Steps:

1. Select the volume.
2. Click **Actions → Attach Volume**.
3. Choose an EC2 instance.
4. Specify a device name.
5. Click **Attach**.

Example device:

```text
/dev/xvdf
```

---

# 🐧 Mounting an EBS Volume (Linux)

### Step 1: Check available disks

```bash
lsblk
```

---

### Step 2: Create a filesystem

```bash
sudo mkfs.ext4 /dev/xvdf
```

---

### Step 3: Create a mount point

```bash
sudo mkdir /data
```

---

### Step 4: Mount the volume

```bash
sudo mount /dev/xvdf /data
```

---

### Step 5: Verify

```bash
df -h
```

---

# 📈 Resizing an EBS Volume

AWS allows increasing:

- Volume Size
- IOPS
- Throughput

Steps:

1. Select the volume.
2. Click **Modify Volume**.
3. Increase the size.
4. Save changes.

Then resize the filesystem inside Linux.

Example:

```bash
sudo resize2fs /dev/xvdf
```

---

# 📸 EBS Snapshots

Snapshots are incremental backups stored in Amazon S3.

Benefits:

- Backup
- Disaster Recovery
- Migration
- Clone Volumes

Example:

```
Volume
   │
   ▼
Snapshot
   │
   ▼
New Volume
```

---

# 🔄 Restoring from a Snapshot

Process:

```
Snapshot
    │
    ▼
Create New Volume
    │
    ▼
Attach to EC2
```

---

# 🔐 EBS Encryption

Amazon EBS supports encryption using **AWS Key Management Service (KMS)**.

Encrypted components:

- Volumes
- Snapshots
- Data in transit
- Data at rest

Benefits:

- Secure storage
- Compliance
- Automatic encryption/decryption

---

# 📊 Monitoring Amazon EBS

Amazon CloudWatch provides metrics such as:

- 📈 Read Operations
- 📉 Write Operations
- ⚡ Read Latency
- ⚡ Write Latency
- 💾 Volume Queue Length
- 📦 Burst Balance

---

# 💻 Useful AWS CLI Commands

### List volumes

```bash
aws ec2 describe-volumes
```

---

### Create a volume

```bash
aws ec2 create-volume \
--availability-zone ap-south-1a \
--size 20 \
--volume-type gp3
```

---

### Attach a volume

```bash
aws ec2 attach-volume \
--volume-id vol-xxxxxxxx \
--instance-id i-xxxxxxxx \
--device /dev/xvdf
```

---

### Create a snapshot

```bash
aws ec2 create-snapshot \
--volume-id vol-xxxxxxxx
```

---

### List snapshots

```bash
aws ec2 describe-snapshots --owner-ids self
```

---

# 💡 Amazon EBS Best Practices

✅ Use **gp3** for most workloads.

✅ Enable encryption.

✅ Take regular snapshots.

✅ Delete unused snapshots.

✅ Tag all volumes.

✅ Monitor CloudWatch metrics.

✅ Resize instead of creating unnecessary volumes.

✅ Use Multi-AZ solutions for high availability.

---

# 🌍 Common Use Cases

| Use Case | Recommended Volume |
|-----------|-------------------|
| Web Server | gp3 |
| Database | io2 |
| Development | gp3 |
| Backup Storage | sc1 |
| Big Data | st1 |
| Application Server | gp3 |

---

# 📝 Key Takeaways

- Amazon EBS is persistent block storage.
- EBS survives EC2 stop/start.
- Snapshots provide incremental backups.
- Encryption uses AWS KMS.
- gp3 is the recommended default volume type.
- Monitor EBS using CloudWatch.

---

# 📋 Summary

In this chapter, you learned:

- Amazon EBS
- Volume Types
- EBS vs Instance Store
- Creating Volumes
- Mounting Volumes
- Resizing
- Snapshots
- Encryption
- Monitoring
- AWS CLI
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Amazon EBS?
2. Is EBS persistent storage?
3. What is the default recommended EBS volume type?
4. What is an EBS Snapshot?
5. Can an EBS volume be detached?

---

## Intermediate

6. Explain gp3 vs io2.
7. What is the difference between EBS and Instance Store?
8. Why must an EBS volume be in the same Availability Zone?
9. How do snapshots work?
10. How do you resize an EBS volume?

---

## Advanced

11. Explain EBS encryption.
12. How would you migrate an EBS volume to another Region?
13. Design a backup strategy using snapshots.
14. Which volume type would you choose for a production database and why?

---

# 🎯 Practice Exercises

## Exercise 1

Create a **10 GB gp3** volume.

---

## Exercise 2

Attach the volume to an EC2 instance.

---

## Exercise 3

Format and mount the volume on Linux.

---

## Exercise 4

Create an EBS Snapshot.

---

## Exercise 5

Increase the volume size from **10 GB** to **20 GB** and resize the filesystem.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
ebs-storage-guide.md
```

Include:

- Amazon EBS Architecture
- Volume Types Comparison
- EBS vs Instance Store
- Snapshot Workflow
- Linux Mount Commands
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Amazon EBS storage guide"
```

---

# 📚 Further Reading

- Amazon EBS Documentation
- EBS Volume Types
- EBS Pricing
- AWS KMS Documentation
- CloudWatch Metrics for EBS
- AWS CLI EC2 Reference

---

# 🚀 What's Next?

In **Chapter 06 – Amazon S3 (Simple Storage Service)**, you'll learn:

- 🪣 What is Amazon S3?
- 🏗️ Buckets and Objects
- 📂 Storage Classes
- 🔐 Bucket Policies and ACLs
- 🌐 Static Website Hosting
- 🔄 Versioning
- ♻️ Lifecycle Rules
- 📦 Object Lock
- 🌍 Cross-Region Replication
- 💻 AWS CLI Commands
- 🛡️ Security Best Practices
