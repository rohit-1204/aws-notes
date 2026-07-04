# AWS Notes
# Chapter 17 - Amazon RDS (Relational Database Service)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Amazon RDS?
2. Why Use Amazon RDS?
3. Self-Managed Database vs RDS
4. Supported Database Engines
5. RDS Components
6. DB Instances
7. Storage Types
8. Multi-AZ Deployment
9. Read Replicas
10. Backups and Snapshots
11. High Availability
12. Security
13. Monitoring
14. RDS Architecture
15. AWS CLI Commands
16. Best Practices
17. Common Use Cases
18. Summary
19. Interview Questions
20. Practice Exercises
21. Mini Project
22. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon RDS
- Create and manage database instances
- Configure backups and snapshots
- Understand Multi-AZ deployments
- Configure Read Replicas
- Secure and monitor databases

---

# 📖 What is Amazon RDS?

**Amazon Relational Database Service (RDS)** is a fully managed database service that makes it easy to set up, operate, and scale relational databases in AWS.

Instead of installing and maintaining a database server yourself, AWS handles most administrative tasks.

RDS manages:

- ⚙️ Installation
- 🔄 Updates
- 💾 Backups
- 📈 Scaling
- 🛡️ High Availability
- 📊 Monitoring

---

# 💡 Why Use Amazon RDS?

Without RDS:

```text
Install OS
      │
Install Database
      │
Configure Storage
      │
Take Backups
      │
Monitor Server
      │
Apply Security Updates
```

Everything must be managed manually.

---

With RDS:

```text
Create Database

↓

AWS Handles

✔ Installation
✔ Backups
✔ Updates
✔ Monitoring
✔ Failover
```

---

# ⚖️ Self-Managed Database vs Amazon RDS

| Self-Managed | Amazon RDS |
|--------------|------------|
| Manual installation | Fully managed |
| Manual backups | Automated backups |
| Manual patching | Automatic patching |
| Manual monitoring | CloudWatch integration |
| Manual failover | Automatic failover |
| Higher maintenance | Lower maintenance |

---

# 🗄️ Supported Database Engines

Amazon RDS supports multiple database engines.

| Database Engine | Supported |
|-----------------|-----------|
| MySQL | ✅ |
| PostgreSQL | ✅ |
| MariaDB | ✅ |
| Oracle Database | ✅ |
| Microsoft SQL Server | ✅ |
| Amazon Aurora | ✅ |

---

# 🧩 RDS Components

Amazon RDS consists of:

- 🗄️ DB Instance
- 💾 Storage
- 📦 Snapshots
- 🔄 Automated Backups
- 🌍 Multi-AZ Deployment
- 📖 Read Replicas
- 📊 Monitoring
- 🔐 Security Groups

---

# 🖥️ DB Instance

A **DB Instance** is the compute resource that runs your database engine.

It includes:

- CPU
- Memory
- Storage
- Database Engine
- Network Configuration

Example:

```text
Engine:
PostgreSQL

Instance:
db.t3.micro

Storage:
20 GB SSD
```

---

# 💾 Storage Types

Amazon RDS offers different storage options.

| Storage Type | Use Case |
|--------------|----------|
| General Purpose SSD (gp3) | Most workloads |
| Provisioned IOPS SSD | High-performance databases |
| Magnetic (Legacy) | Older workloads |

---

# 🌍 Multi-AZ Deployment

Multi-AZ improves availability by creating a standby database in another Availability Zone.

```text
Application
      │
      ▼
Primary Database
      │
Synchronous Replication
      ▼
Standby Database
```

If the primary instance fails, AWS automatically switches to the standby instance.

Benefits:

- ✅ High Availability
- ✅ Automatic Failover
- ✅ Better Reliability

---

# 📖 Read Replicas

Read Replicas improve read performance.

```text
Application
      │
      ▼
Primary Database
      │
Asynchronous Replication
      ▼
Read Replica
```

Read Replicas are useful for:

- Reporting
- Analytics
- Read-heavy applications

---

# 💾 Automated Backups

RDS automatically creates backups during the backup window.

Includes:

- Database
- Transaction Logs

Retention Period:

- 1–35 Days

---

# 📸 Snapshots

Snapshots are manual backups.

Features:

- Stored in Amazon S3
- Can be retained indefinitely
- Used for disaster recovery
- Can restore new database instances

---

# 🔄 Backup vs Snapshot

| Backup | Snapshot |
|----------|----------|
| Automatic | Manual |
| Retention period | Permanent until deleted |
| Scheduled | On-demand |
| Continuous | Point-in-time backup |

---

# 🛡️ High Availability

High Availability combines:

- Multi-AZ
- Automatic Failover
- Automated Backups

```text
Users
  │
Application
  │
Primary DB
  │
Replication
  ▼
Standby DB
```

---

# 🔐 Security

Amazon RDS supports:

- Security Groups
- IAM Authentication
- SSL Connections
- Encryption at Rest
- Encryption in Transit
- KMS Integration

Never expose your database directly to the internet unless absolutely necessary.

---

# 📊 Monitoring

Amazon RDS integrates with CloudWatch.

Common metrics:

- CPU Utilization
- Free Storage Space
- Database Connections
- Read IOPS
- Write IOPS
- Network Throughput

---

# 🏗️ Amazon RDS Architecture

```text
                 Users
                    │
                    ▼
            Application Server
                    │
                    ▼
              Amazon RDS
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
   Primary Database      Standby Database
         │
         ▼
    Read Replica
```

---

# 💻 Useful AWS CLI Commands

## List DB Instances

```bash
aws rds describe-db-instances
```

---

## Create a Database

```bash
aws rds create-db-instance \
--db-instance-identifier mydb \
--db-instance-class db.t3.micro \
--engine mysql
```

---

## List Snapshots

```bash
aws rds describe-db-snapshots
```

---

## Create Snapshot

```bash
aws rds create-db-snapshot \
--db-instance-identifier mydb \
--db-snapshot-identifier mydb-backup
```

---

## Delete Database

```bash
aws rds delete-db-instance \
--db-instance-identifier mydb
```

---

# 💡 Best Practices

✅ Enable Multi-AZ for production databases.

✅ Enable automatic backups.

✅ Use Read Replicas for read-heavy workloads.

✅ Encrypt storage using AWS KMS.

✅ Keep databases in private subnets.

✅ Monitor with Amazon CloudWatch.

✅ Use IAM authentication where supported.

✅ Regularly test database restoration.

---

# 🌍 Common Use Cases

| Scenario | Recommended Feature |
|----------|---------------------|
| Production Database | Multi-AZ |
| Reporting | Read Replica |
| Disaster Recovery | Snapshots |
| Development | Single-AZ |
| E-commerce | Multi-AZ + Read Replicas |
| Analytics | Read Replicas |

---

# 📝 Key Takeaways

- Amazon RDS is a managed relational database service.
- AWS handles backups, patching, and maintenance.
- Multi-AZ improves availability.
- Read Replicas improve read performance.
- Snapshots provide manual backups.
- CloudWatch monitors database performance.

---

# 📋 Summary

In this chapter, you learned:

- Amazon RDS
- Supported Database Engines
- DB Instances
- Storage Types
- Multi-AZ Deployment
- Read Replicas
- Automated Backups
- Snapshots
- Security
- Monitoring
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Amazon RDS?
2. Name supported RDS database engines.
3. What is a DB Instance?
4. What is Multi-AZ?
5. What is a Read Replica?

---

## Intermediate

6. Explain the difference between Multi-AZ and Read Replica.
7. What is the difference between backups and snapshots?
8. How does automatic failover work?
9. Why should RDS be deployed in private subnets?
10. What metrics can CloudWatch monitor?

---

## Advanced

11. Design a highly available database architecture using RDS.
12. How would you improve database read performance?
13. Explain synchronous vs asynchronous replication.
14. How would you secure an Amazon RDS database?
15. How would you migrate an on-premises database to Amazon RDS?

---

# 🎯 Practice Exercises

## Exercise 1

Create a MySQL RDS instance.

---

## Exercise 2

Enable automated backups.

---

## Exercise 3

Create a manual snapshot.

---

## Exercise 4

Launch a Read Replica.

---

## Exercise 5

Enable Multi-AZ deployment and observe the configuration.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-rds-guide.md
```

Include:

- Amazon RDS Overview
- Supported Engines
- DB Instances
- Storage Types
- Multi-AZ
- Read Replicas
- Backups
- Snapshots
- Security
- Monitoring
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Amazon RDS guide"
```

---

# 📚 Further Reading

- Amazon RDS Documentation
- Amazon Aurora User Guide
- AWS Database Best Practices
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 18 – AWS IAM (Identity and Access Management)**, you'll learn:

- 👤 What is IAM?
- 👥 Users, Groups & Roles
- 🔑 Policies
- 🔒 Authentication vs Authorization
- 🛡️ IAM Best Practices
- 🔐 MFA
- 🌐 Cross-Account Access
- 💻 AWS CLI Commands
- 🏆 Security Recommendations
