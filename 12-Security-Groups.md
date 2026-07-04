# AWS Notes
# Chapter 12 - Security Groups

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What are Security Groups?
2. Why Do We Need Security Groups?
3. How Security Groups Work
4. Stateful Firewall
5. Inbound Rules
6. Outbound Rules
7. Security Group Architecture
8. Common Ports
9. Creating Security Groups
10. Security Groups for Different AWS Services
11. Security Groups vs Network ACLs
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

- Understand Security Groups
- Configure inbound and outbound rules
- Secure EC2 instances
- Apply least privilege access
- Differentiate Security Groups and Network ACLs
- Build secure AWS network architectures

---

# 📖 What are Security Groups?

A **Security Group (SG)** is a **virtual firewall** that controls network traffic to and from AWS resources.

It protects resources such as:

- 🖥️ EC2 Instances
- 🗄️ RDS Databases
- ⚖️ Load Balancers
- 📦 ECS Tasks
- ☸️ EKS Worker Nodes
- 📁 Elastic File System (EFS)

Think of a Security Group as a security guard standing at the entrance of your AWS resource.

---

# 💡 Why Do We Need Security Groups?

Security Groups help:

- 🔒 Protect servers
- 🚫 Block unauthorized access
- 🌐 Allow only required traffic
- 🛡️ Improve security
- 📜 Follow security best practices

Without Security Groups, your AWS resources could be exposed to attacks.

---

# 🧠 How Security Groups Work

Traffic Flow:

```text
Internet
     │
     ▼
Security Group
     │
     ▼
EC2 Instance
```

Every incoming and outgoing packet is checked against the Security Group rules.

If a rule matches:

✅ Traffic is allowed.

Otherwise:

❌ Traffic is denied.

---

# 🛡️ Security Groups are Stateful

Security Groups are **Stateful Firewalls**.

This means:

If an incoming request is allowed,

the response is automatically allowed.

Example:

```text
Laptop
   │ SSH
   ▼
Security Group
   │
EC2 Instance
   │
Automatic Response
   ▼
Laptop
```

No additional outbound rule is required for the response.

---

# 🚪 Inbound Rules

Inbound Rules control **incoming traffic**.

Example:

| Port | Protocol | Source | Purpose |
|------|----------|---------|----------|
| 22 | TCP | Your IP | SSH |
| 80 | TCP | 0.0.0.0/0 | HTTP |
| 443 | TCP | 0.0.0.0/0 | HTTPS |

---

# 🚀 Outbound Rules

Outbound Rules control **traffic leaving** the resource.

By default:

AWS allows **all outbound traffic**.

Example:

| Port | Destination | Purpose |
|------|-------------|----------|
| All | 0.0.0.0/0 | Internet Access |

---

# 🏗️ Security Group Architecture

```text
                Internet
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
     HTTP(80)               HTTPS(443)
        │                       │
        ▼                       ▼
          Security Group
                │
                ▼
            EC2 Instance
```

---

# 🌐 Common Ports

| Port | Service |
|------|----------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 27017 | MongoDB |
| 3389 | RDP (Windows) |

---

# 🖥️ Creating a Security Group

Steps:

1. Open **EC2 Console**
2. Click **Security Groups**
3. Select **Create Security Group**
4. Enter Name and Description
5. Choose a VPC
6. Add Inbound Rules
7. Add Outbound Rules
8. Click **Create Security Group**

---

# 🔐 Example Security Groups

## Web Server

| Type | Port | Source |
|------|------|---------|
| SSH | 22 | Your IP |
| HTTP | 80 | 0.0.0.0/0 |
| HTTPS | 443 | 0.0.0.0/0 |

---

## Database Server

| Type | Port | Source |
|------|------|---------|
| MySQL | 3306 | Web Server SG |

Notice:

The database is **not exposed** to the Internet.

---

## Bastion Host

| Type | Port | Source |
|------|------|---------|
| SSH | 22 | Your Public IP |

---

# 🔗 Security Group Referencing

Instead of allowing an IP address,

AWS allows one Security Group to reference another.

Example:

```text
Web Security Group
        │
        ▼
Database Security Group
```

Only EC2 instances in the Web Security Group can access the database.

---

# ⚖️ Security Groups vs Network ACLs

| Security Group | Network ACL |
|----------------|-------------|
| Instance Level | Subnet Level |
| Stateful | Stateless |
| Allow Rules Only | Allow & Deny Rules |
| Easier to Configure | More Granular Control |

---

# 🚫 Common Mistakes

❌ Opening SSH to:

```text
0.0.0.0/0
```

Instead:

```text
Your Public IP
```

---

❌ Opening Database Ports to Everyone

Wrong:

```text
3306 → 0.0.0.0/0
```

Correct:

```text
3306 → Web Server Security Group
```

---

❌ Allowing All Traffic

Avoid using:

```text
All Traffic
0.0.0.0/0
```

Unless absolutely necessary.

---

# 💻 Useful AWS CLI Commands

## List Security Groups

```bash
aws ec2 describe-security-groups
```

---

## Create a Security Group

```bash
aws ec2 create-security-group \
--group-name WebServerSG \
--description "Web Server Security Group" \
--vpc-id vpc-xxxxxxxx
```

---

## Add an Inbound Rule

```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 22 \
--cidr YOUR_PUBLIC_IP/32
```

---

## Remove an Inbound Rule

```bash
aws ec2 revoke-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 22 \
--cidr YOUR_PUBLIC_IP/32
```

---

## Delete a Security Group

```bash
aws ec2 delete-security-group \
--group-id sg-xxxxxxxx
```

---

# 💡 Best Practices

✅ Follow the Principle of Least Privilege.

✅ Open only required ports.

✅ Restrict SSH access to your IP.

✅ Keep databases in Private Subnets.

✅ Use Security Group references instead of IPs.

✅ Regularly review unused Security Groups.

✅ Avoid using:

```text
0.0.0.0/0
```

unless required.

---

# 🌍 Common Use Cases

| Resource | Security Group Rules |
|-----------|----------------------|
| Web Server | HTTP, HTTPS, SSH |
| Database | MySQL from App SG |
| Bastion Host | SSH from Admin IP |
| Load Balancer | HTTP/HTTPS |
| Redis | Port 6379 from App SG |
| Application Server | HTTP from ALB SG |

---

# 📝 Key Takeaways

- Security Groups are virtual firewalls.
- They operate at the instance level.
- Security Groups are stateful.
- Only Allow rules are supported.
- Restrict access using the least privilege principle.
- Security Group references improve security.

---

# 📋 Summary

In this chapter, you learned:

- Security Groups
- Stateful Firewall
- Inbound Rules
- Outbound Rules
- Security Group Referencing
- Common Ports
- Security Groups vs NACLs
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Security Group?
2. Why are Security Groups required?
3. Are Security Groups stateful or stateless?
4. What is the default outbound rule?
5. Can Security Groups deny traffic?

---

## Intermediate

6. Explain inbound and outbound rules.
7. What is Security Group referencing?
8. Why shouldn't databases allow public access?
9. Differentiate Security Groups and NACLs.
10. Can one EC2 instance have multiple Security Groups?

---

## Advanced

11. Design Security Groups for a three-tier application.
12. Explain how Security Groups process traffic.
13. How would you secure SSH access to production servers?
14. What are common Security Group misconfigurations?

---

# 🎯 Practice Exercises

## Exercise 1

Create a Security Group named:

```text
WebServerSG
```

---

## Exercise 2

Allow:

- SSH (22) from your public IP
- HTTP (80) from anywhere
- HTTPS (443) from anywhere

---

## Exercise 3

Create another Security Group:

```text
DatabaseSG
```

Allow:

```text
MySQL (3306)
```

Only from:

```text
WebServerSG
```

---

## Exercise 4

Launch an EC2 instance and attach:

```text
WebServerSG
```

Verify SSH connectivity.

---

## Exercise 5

Remove the SSH rule and verify that SSH access is denied.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-security-groups-guide.md
```

Include:

- Security Group Overview
- Architecture Diagram
- Inbound Rules
- Outbound Rules
- Common Ports
- Web Server SG
- Database SG
- Security Group Referencing
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add AWS Security Groups guide"
```

---

# 📚 Further Reading

- AWS Security Groups Documentation
- Amazon EC2 User Guide
- VPC Security Best Practices
- AWS Well-Architected Framework
- AWS Networking Guide

---

# 🚀 What's Next?

In **Chapter 13 – Network ACLs (NACLs)**, you'll learn:

- 🛡️ What is a Network ACL?
- 🔄 Stateless Firewalls
- 🚪 Inbound & Outbound Rules
- 🔢 Rule Numbers and Evaluation
- ⚖️ NACL vs Security Groups
- 🏗️ Subnet-Level Security
- 💻 AWS CLI Commands
- 🔒 Best Practices
