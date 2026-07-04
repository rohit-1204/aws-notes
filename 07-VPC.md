# AWS Notes
# Chapter 07 - Amazon VPC (Virtual Private Cloud)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 90–120 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Amazon VPC?
2. Why Use VPC?
3. VPC Architecture
4. CIDR Blocks
5. Public and Private Subnets
6. Route Tables
7. Internet Gateway (IGW)
8. NAT Gateway
9. Security Groups
10. Network ACLs
11. Elastic Network Interface (ENI)
12. VPC Endpoints
13. VPC Peering
14. Transit Gateway
15. Flow Logs
16. Default VPC vs Custom VPC
17. Building a Production VPC
18. AWS CLI Commands
19. Best Practices
20. Common Use Cases
21. Summary
22. Interview Questions
23. Practice Exercises
24. Mini Project
25. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon VPC
- Create a custom VPC
- Design public and private subnets
- Configure Internet and NAT Gateways
- Understand Route Tables
- Secure a VPC using Security Groups and NACLs
- Connect multiple VPCs
- Monitor traffic using Flow Logs
- Build a production-ready AWS network

---

# 📖 What is Amazon VPC?

Amazon **Virtual Private Cloud (VPC)** is a logically isolated virtual network inside AWS where you launch AWS resources.

A VPC gives you complete control over:

- 🌐 IP Address Range
- 🛣️ Routing
- 🔐 Security
- 🌍 Internet Connectivity
- 🔄 Network Traffic

Think of a VPC as your own private data center inside AWS.

---

# 💡 Why Use Amazon VPC?

Amazon VPC provides:

- 🔒 Network Isolation
- 🌐 Custom IP Addressing
- 🛡️ Secure Communication
- 📈 High Availability
- ⚡ Scalable Infrastructure
- 🔄 Hybrid Cloud Connectivity

---

# 🏗️ Amazon VPC Architecture

```text
                        Internet
                            │
                    🌍 Internet Gateway
                            │
        ┌───────────────────┴───────────────────┐
        │                                       │
        ▼                                       ▼
  🌐 Public Subnet                       🔐 Private Subnet
        │                                       │
    EC2 + ALB                            EC2 + Database
        │                                       │
        └───────────────NAT Gateway─────────────┘
                            │
                            ▼
                       Amazon S3
```

---

# 🧠 Understanding CIDR Blocks

A CIDR block defines the IP address range for your VPC.

Example:

```text
10.0.0.0/16
```

Breakdown:

| CIDR | Number of IP Addresses |
|------|------------------------|
| /16 | 65,536 |
| /24 | 256 |
| /28 | 16 |

Example:

```
VPC
10.0.0.0/16

Public Subnet
10.0.1.0/24

Private Subnet
10.0.2.0/24
```

---

# 🌐 Public and Private Subnets

## 🌍 Public Subnet

Has a route to the Internet Gateway.

Resources:

- Web Servers
- Load Balancers
- Bastion Hosts

---

## 🔐 Private Subnet

No direct internet access.

Resources:

- Databases
- Backend APIs
- Internal Services
- Application Servers

---

# 🏠 Example Network Layout

```text
VPC (10.0.0.0/16)

├── Public Subnet A
│      10.0.1.0/24
│      EC2
│      Load Balancer
│
├── Public Subnet B
│      10.0.2.0/24
│
├── Private Subnet A
│      10.0.11.0/24
│      Database
│
└── Private Subnet B
       10.0.12.0/24
```

---

# 🛣️ Route Tables

A Route Table determines where network traffic is sent.

Example:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

Private subnet:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | NAT Gateway |

---

# 🌍 Internet Gateway (IGW)

An Internet Gateway allows communication between your VPC and the Internet.

Functions:

- Incoming Internet Traffic
- Outgoing Internet Traffic

Without an IGW, public instances cannot access the Internet.

---

# 🔄 NAT Gateway

A NAT Gateway allows **private subnet resources** to access the Internet **without being publicly accessible**.

Example:

```text
Private EC2
      │
      ▼
 NAT Gateway
      │
      ▼
 Internet
```

Use Cases:

- Software Updates
- Package Installation
- API Calls

---

# 🔐 Security Groups

A Security Group is a **stateful virtual firewall**.

Controls:

- Inbound Rules
- Outbound Rules

Example:

| Port | Protocol | Purpose |
|------|----------|----------|
| 22 | SSH | Linux Login |
| 80 | HTTP | Website |
| 443 | HTTPS | Secure Website |

Characteristics:

- Stateful
- Allow rules only
- Attached to EC2 instances

---

# 🛡️ Network ACL (NACL)

A Network ACL is a **stateless firewall** for subnets.

Controls:

- Allow Rules
- Deny Rules

Characteristics:

- Stateless
- Supports Allow & Deny
- Applied to Subnets

---

# ⚖️ Security Group vs NACL

| Security Group | Network ACL |
|----------------|-------------|
| Instance Level | Subnet Level |
| Stateful | Stateless |
| Allow Only | Allow & Deny |
| Easier to Manage | More Granular |

---

# 🔌 Elastic Network Interface (ENI)

An ENI is a virtual network card attached to an EC2 instance.

Contains:

- Private IP
- Public IP (optional)
- MAC Address
- Security Groups

---

# 🔗 VPC Endpoints

VPC Endpoints allow private communication with AWS services without using the Internet.

Examples:

- Amazon S3
- DynamoDB

Benefits:

- Improved Security
- Reduced Latency
- No Internet Gateway Required

---

# 🌉 VPC Peering

VPC Peering connects two VPCs.

Example:

```text
VPC A
   │
VPC Peering
   │
VPC B
```

Use Cases:

- Multi-team architecture
- Shared services
- Development and Production communication

---

# 🚉 Transit Gateway

Transit Gateway connects multiple VPCs and on-premises networks.

```text
        Transit Gateway
        /      |      \
      VPC1   VPC2   VPN
```

Benefits:

- Simplified networking
- Centralized routing
- Easy scalability

---

# 📋 VPC Flow Logs

Flow Logs capture information about network traffic.

Useful for:

- Security Auditing
- Troubleshooting
- Compliance
- Monitoring

---

# 🏢 Default VPC vs Custom VPC

| Default VPC | Custom VPC |
|-------------|------------|
| Created automatically | Created manually |
| Public subnet by default | Fully customizable |
| Easy for beginners | Recommended for production |

---

# 🏗️ Production VPC Design

```text
                   Internet
                       │
               Internet Gateway
                       │
              Public Route Table
                       │
        ┌──────────────┴──────────────┐
        ▼                             ▼
 Public Subnet A               Public Subnet B
      ALB                          NAT Gateway
        │
        ▼
 Private Subnet A          Private Subnet B
 App Servers               App Servers
        │
        ▼
 Database Subnets (RDS)
```

---

# 💻 Useful AWS CLI Commands

### List VPCs

```bash
aws ec2 describe-vpcs
```

---

### Create a VPC

```bash
aws ec2 create-vpc \
--cidr-block 10.0.0.0/16
```

---

### Create a Subnet

```bash
aws ec2 create-subnet \
--vpc-id vpc-xxxx \
--cidr-block 10.0.1.0/24
```

---

### Describe Route Tables

```bash
aws ec2 describe-route-tables
```

---

### Create an Internet Gateway

```bash
aws ec2 create-internet-gateway
```

---

### Attach an Internet Gateway

```bash
aws ec2 attach-internet-gateway \
--internet-gateway-id igw-xxxx \
--vpc-id vpc-xxxx
```

---

# 💡 Amazon VPC Best Practices

✅ Use private subnets for databases.

✅ Deploy resources across multiple Availability Zones.

✅ Use Security Groups with least privilege.

✅ Enable VPC Flow Logs.

✅ Use NAT Gateway instead of exposing private servers.

✅ Use custom VPCs for production.

✅ Tag all networking resources.

---

# 🌍 Common Use Cases

| Use Case | AWS Components |
|-----------|----------------|
| Web Application | VPC + Public Subnet + ALB |
| Database | Private Subnet + RDS |
| Kubernetes | VPC + EKS |
| Hybrid Cloud | VPN + Transit Gateway |
| Secure Backend | Private Subnet + NAT Gateway |

---

# 📝 Key Takeaways

- Amazon VPC creates an isolated network in AWS.
- Public subnets connect to the Internet using an Internet Gateway.
- Private subnets use a NAT Gateway for outbound internet access.
- Security Groups secure instances.
- NACLs secure subnets.
- VPC Peering and Transit Gateway connect networks.
- Flow Logs help monitor network traffic.

---

# 📋 Summary

In this chapter, you learned:

- Amazon VPC
- CIDR Blocks
- Public & Private Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- ENIs
- VPC Endpoints
- VPC Peering
- Transit Gateway
- Flow Logs
- Production VPC Design
- AWS CLI Commands

---

# ❓ Interview Questions

## Beginner

1. What is Amazon VPC?
2. What is a subnet?
3. What is a CIDR block?
4. What is an Internet Gateway?
5. What is a NAT Gateway?

---

## Intermediate

6. Explain Security Groups and NACLs.
7. What is the difference between a public and private subnet?
8. Why are Route Tables required?
9. What are VPC Flow Logs?
10. What is VPC Peering?

---

## Advanced

11. Design a highly available VPC architecture.
12. Explain Transit Gateway.
13. How would you secure a production VPC?
14. How would you connect an on-premises network to AWS?

---

# 🎯 Practice Exercises

## Exercise 1

Create a custom VPC with CIDR:

```text
10.0.0.0/16
```

---

## Exercise 2

Create:

- Public Subnet
- Private Subnet

---

## Exercise 3

Attach an Internet Gateway and configure Route Tables.

---

## Exercise 4

Deploy an EC2 instance in the public subnet.

---

## Exercise 5

Deploy another EC2 instance in the private subnet and configure outbound internet access using a NAT Gateway.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-vpc-design.md
```

Include:

- VPC Architecture Diagram
- CIDR Planning
- Public & Private Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- AWS CLI Commands
- Production Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Amazon VPC architecture guide"
```

---

# 📚 Further Reading

- Amazon VPC Documentation
- VPC Best Practices
- AWS Networking Guide
- Transit Gateway Documentation
- VPC Peering Documentation
- AWS CLI EC2 Reference

---

# 🚀 What's Next?

In **Chapter 08 – Elastic Load Balancer (ELB) & Auto Scaling**, you'll learn:

- ⚖️ What is Load Balancing?
- 🌐 Application Load Balancer (ALB)
- 🚀 Network Load Balancer (NLB)
- 🔄 Gateway Load Balancer (GWLB)
- 📈 Auto Scaling Groups (ASG)
- ❤️ Health Checks
- 🎯 Target Groups
- 📊 Scaling Policies
- 💻 AWS CLI Commands
- 🏗️ Highly Available Architecture
