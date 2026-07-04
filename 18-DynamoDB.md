# AWS Notes
# Chapter 18 - Amazon DynamoDB

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Amazon DynamoDB?
2. Why Use DynamoDB?
3. SQL vs NoSQL
4. DynamoDB Components
5. Tables, Items & Attributes
6. Primary Keys
7. Secondary Indexes
8. Read & Write Capacity
9. On-Demand vs Provisioned Capacity
10. DynamoDB Accelerator (DAX)
11. Streams
12. Time To Live (TTL)
13. Backup & Restore
14. Security
15. DynamoDB Architecture
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

- Understand Amazon DynamoDB
- Differentiate SQL and NoSQL databases
- Design DynamoDB tables
- Configure partition and sort keys
- Use secondary indexes
- Understand scaling and performance
- Secure DynamoDB tables

---

# 📖 What is Amazon DynamoDB?

Amazon **DynamoDB** is a **fully managed NoSQL database service** provided by AWS.

Unlike relational databases, DynamoDB stores data as **key-value pairs** and **documents**.

AWS automatically manages:

- ⚙️ Infrastructure
- 📈 Scaling
- 💾 Storage
- 🔄 Replication
- 🛡️ High Availability
- 📊 Performance

---

# 💡 Why Use DynamoDB?

Without DynamoDB:

```text
Install Database

↓

Configure Cluster

↓

Manage Replication

↓

Scale Servers

↓

Monitor Performance
```

Everything is managed manually.

---

With DynamoDB:

```text
Create Table

↓

AWS Automatically

✔ Scales
✔ Replicates
✔ Backs Up
✔ Secures
✔ Monitors
```

---

# ⚖️ SQL vs NoSQL

| SQL Database | NoSQL Database |
|--------------|----------------|
| Fixed Schema | Flexible Schema |
| Tables & Rows | Tables, Items & Attributes |
| Complex Joins | No Joins |
| Vertical Scaling | Horizontal Scaling |
| Structured Data | Semi-Structured Data |

---

# 🧠 DynamoDB Components

DynamoDB consists of:

- 📋 Tables
- 📄 Items
- 🏷️ Attributes
- 🔑 Primary Keys
- 📚 Secondary Indexes
- 🌊 Streams
- ⚡ DAX
- ⏳ TTL

---

# 📋 Tables

A **Table** stores related data.

Example:

```
Employees
```

```
Employees Table
```

| EmployeeID | Name | Department |
|------------|------|------------|
| 101 | Alice | HR |
| 102 | Bob | IT |

---

# 📄 Items

An **Item** is similar to a row in a relational database.

Example:

```json
{
  "EmployeeID": 101,
  "Name": "Alice",
  "Department": "HR"
}
```

Each item can have different attributes.

---

# 🏷️ Attributes

Attributes are the properties of an item.

Example:

```json
{
  "EmployeeID":101,
  "Name":"Alice",
  "Age":25,
  "Salary":45000
}
```

Unlike SQL, every item does **not** need identical attributes.

---

# 🔑 Primary Keys

Every DynamoDB table requires a primary key.

Two types are available.

---

## Partition Key

A single unique attribute.

Example:

```text
EmployeeID

101
102
103
```

AWS uses the partition key to distribute data.

---

## Composite Primary Key

Consists of:

- Partition Key
- Sort Key

Example:

```
Partition Key : CustomerID

Sort Key : OrderID
```

| CustomerID | OrderID |
|------------|----------|
| C101 | O1001 |
| C101 | O1002 |
| C102 | O2001 |

---

# 📚 Secondary Indexes

Indexes improve query flexibility.

Types:

- Global Secondary Index (GSI)
- Local Secondary Index (LSI)

---

## Global Secondary Index (GSI)

Allows querying using attributes other than the primary key.

Example:

```
Primary Key

EmployeeID

Search Using

Department
```

---

## Local Secondary Index (LSI)

Uses the same partition key but a different sort key.

Useful for sorting data differently.

---

# 📈 Read & Write Capacity

DynamoDB supports two capacity modes.

- Provisioned Capacity
- On-Demand Capacity

---

# ⚙️ Provisioned Capacity

You specify:

- Read Capacity Units (RCU)
- Write Capacity Units (WCU)

Example:

```text
Reads : 20

Writes : 10
```

Suitable for predictable workloads.

---

# ⚡ On-Demand Capacity

AWS automatically adjusts capacity based on traffic.

Benefits:

- No capacity planning
- Automatic scaling
- Pay only for requests

Ideal for unpredictable workloads.

---

# 🚀 DynamoDB Accelerator (DAX)

**DAX** is an in-memory cache for DynamoDB.

Benefits:

- Microsecond latency
- Faster reads
- Reduced database load

Architecture:

```text
Application

↓

DAX Cache

↓

DynamoDB
```

---

# 🌊 DynamoDB Streams

Streams capture data changes.

Supported events:

- Insert
- Modify
- Delete

Useful for:

- Auditing
- Event processing
- Lambda triggers

---

# ⏳ Time To Live (TTL)

TTL automatically deletes expired items.

Example:

```
Session Token

Expires After

24 Hours

↓

Automatically Deleted
```

Useful for:

- Login sessions
- Temporary files
- Cache entries

---

# 💾 Backup & Restore

Amazon DynamoDB supports:

- On-demand backups
- Point-in-Time Recovery (PITR)

Benefits:

- Disaster recovery
- Data protection
- Easy restoration

---

# 🔐 Security

DynamoDB supports:

- IAM Policies
- Encryption at Rest
- Encryption in Transit
- AWS KMS
- VPC Endpoints
- CloudTrail Logging

---

# 🏗️ DynamoDB Architecture

```text
                Application
                     │
                     ▼
                Amazon API
                     │
         ┌───────────┴───────────┐
         ▼                       ▼
     DynamoDB Table         DynamoDB Streams
         │
         ▼
        DAX Cache
```

---

# 💻 Useful AWS CLI Commands

## Create Table

```bash
aws dynamodb create-table \
--table-name Employees
```

---

## List Tables

```bash
aws dynamodb list-tables
```

---

## Describe Table

```bash
aws dynamodb describe-table \
--table-name Employees
```

---

## Insert Item

```bash
aws dynamodb put-item \
--table-name Employees \
--item file://employee.json
```

---

## Scan Table

```bash
aws dynamodb scan \
--table-name Employees
```

---

## Delete Table

```bash
aws dynamodb delete-table \
--table-name Employees
```

---

# 💡 Best Practices

✅ Choose partition keys carefully.

✅ Avoid hot partitions.

✅ Use On-Demand mode for unpredictable workloads.

✅ Enable Point-in-Time Recovery.

✅ Enable encryption using AWS KMS.

✅ Use GSIs only when required.

✅ Use TTL for temporary data.

✅ Monitor using CloudWatch.

---

# 🌍 Common Use Cases

| Application | DynamoDB |
|--------------|----------|
| Gaming | ✅ |
| Shopping Cart | ✅ |
| User Sessions | ✅ |
| IoT Applications | ✅ |
| Mobile Apps | ✅ |
| Real-Time Analytics | ✅ |
| Chat Applications | ✅ |

---

# 📝 Key Takeaways

- DynamoDB is a managed NoSQL database.
- Stores key-value and document data.
- Automatically scales.
- Supports Global & Local Secondary Indexes.
- Offers On-Demand and Provisioned capacity.
- Streams enable event-driven applications.
- TTL automatically removes expired items.

---

# 📋 Summary

In this chapter, you learned:

- Amazon DynamoDB
- SQL vs NoSQL
- Tables
- Items
- Attributes
- Primary Keys
- Secondary Indexes
- Capacity Modes
- DAX
- Streams
- TTL
- Security
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Amazon DynamoDB?
2. Is DynamoDB SQL or NoSQL?
3. What is an Item?
4. What is a Partition Key?
5. What is TTL?

---

## Intermediate

6. Explain Provisioned vs On-Demand Capacity.
7. What is a Global Secondary Index?
8. What is DynamoDB Streams?
9. Explain DAX.
10. How does DynamoDB scale?

---

## Advanced

11. Design a scalable shopping cart using DynamoDB.
12. How do you prevent hot partitions?
13. Explain DynamoDB partitioning.
14. Compare DynamoDB and Amazon RDS.
15. Explain Point-in-Time Recovery.

---

# 🎯 Practice Exercises

## Exercise 1

Create a DynamoDB table named:

```
Employees
```

---

## Exercise 2

Insert five employee records.

---

## Exercise 3

Create a Global Secondary Index.

---

## Exercise 4

Enable Point-in-Time Recovery.

---

## Exercise 5

Enable TTL for temporary session records.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-dynamodb-guide.md
```

Include:

- DynamoDB Overview
- SQL vs NoSQL
- Tables & Items
- Primary Keys
- Secondary Indexes
- Capacity Modes
- DAX
- Streams
- TTL
- Security
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add DynamoDB guide"
```

---

# 📚 Further Reading

- Amazon DynamoDB Documentation
- DynamoDB Developer Guide
- AWS NoSQL Database Best Practices
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 19 – AWS IAM (Identity and Access Management)**, you'll learn:

- 👤 IAM Users
- 👥 IAM Groups
- 🎭 IAM Roles
- 📜 IAM Policies
- 🔐 MFA
- 🔑 Access Keys
- 🌐 Cross-Account Access
- 🛡️ Security Best Practices
- 💻 AWS CLI Commands
- 🚀 Hands-on IAM Labs
