# AWS Notes
# Chapter 08 - Amazon VPC Subnets

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 45–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is a Subnet?
2. Why Do We Need Subnets?
3. How Subnets Work
4. Public vs Private Subnets
5. CIDR Blocks and Subnets
6. Creating a Subnet
7. Subnet Routing
8. Availability Zones
9. Public IP Assignment
10. Designing Subnets
11. Best Practices
12. AWS CLI Commands
13. Summary
14. Interview Questions
15. Practice Exercises
16. Mini Project
17. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what a subnet is
- Differentiate between public and private subnets
- Plan subnet CIDR ranges
- Create subnets in AWS
- Associate route tables
- Deploy resources in appropriate subnets
- Design a production-ready subnet architecture

---

# 📖 What is a Subnet?

A **Subnet (Subnetwork)** is a smaller network created from a larger VPC network.

Instead of placing every resource in one large network, we divide the VPC into multiple smaller networks called **subnets**.

Think of a VPC as a city and subnets as different neighborhoods.

---

# 💡 Why Do We Need Subnets?

Subnets help us:

- 🔒 Improve security
- 📈 Increase scalability
- 🌍 Deploy resources across multiple Availability Zones
- ⚡ Improve network performance
- 🛡️ Separate public and private resources

---

# 🏗️ Subnet Architecture

```text
                 VPC
            10.0.0.0/16
                  │
      ┌───────────┴───────────┐
      │                       │
      ▼                       ▼
 Public Subnet          Private Subnet
 10.0.1.0/24             10.0.2.0/24
      │                       │
      ▼                       ▼
 Web Server             Database Server
```

---

# 🧠 Understanding Subnets

Suppose we create a VPC:

```text
10.0.0.0/16
```

We can divide it into multiple subnets.

Example:

| Subnet | CIDR |
|---------|------|
| Public A | 10.0.1.0/24 |
| Public B | 10.0.2.0/24 |
| Private A | 10.0.11.0/24 |
| Private B | 10.0.12.0/24 |

---

# 🌍 Public Subnet

A Public Subnet is connected to the Internet using an **Internet Gateway (IGW).**

Resources placed here can communicate with the Internet.

Common resources:

- 🌐 Web Servers
- ⚖️ Load Balancers
- 🖥️ Bastion Hosts
- 📡 Reverse Proxies

---

# 🔐 Private Subnet

A Private Subnet does **not** have direct Internet access.

Resources here remain hidden from the public Internet.

Common resources:

- 🗄️ Databases
- ⚙️ Backend APIs
- 🔒 Internal Applications
- 📊 Cache Servers

---

# 🔄 Public vs Private Subnet

| Feature | Public | Private |
|----------|---------|----------|
| Internet Access | ✅ Yes | ❌ No |
| Internet Gateway Route | ✅ Yes | ❌ No |
| NAT Gateway Required | ❌ No | ✅ Yes (for outbound access) |
| Accessible from Internet | ✅ Yes | ❌ No |
| Typical Resources | Web Servers | Databases |

---

# 📦 CIDR Blocks

Each subnet receives a portion of the VPC CIDR.

Example:

```
VPC
10.0.0.0/16

Public
10.0.1.0/24

Private
10.0.2.0/24
```

---

# 📏 CIDR Size Comparison

| CIDR | Total IP Addresses |
|------|--------------------|
| /16 | 65,536 |
| /20 | 4,096 |
| /24 | 256 |
| /28 | 16 |

AWS reserves **5 IP addresses** in every subnet.

Example:

```
10.0.1.0/24

Total IPs: 256
Usable IPs: 251
Reserved by AWS: 5
```

---

# 🌎 Availability Zones

Each subnet belongs to **one Availability Zone (AZ).**

Example:

```text
Region: ap-south-1

AZ A
│
└── Public Subnet A

AZ B
│
└── Public Subnet B

AZ C
│
└── Private Subnet C
```

Deploying resources across multiple AZs improves high availability.

---

# 🏗️ Creating a Subnet

Steps:

1. Open **VPC Console**
2. Click **Subnets**
3. Select **Create Subnet**
4. Choose a VPC
5. Select an Availability Zone
6. Enter CIDR Block
7. Click **Create**

---

# 🛣️ Route Tables

A subnet becomes **Public** or **Private** based on its Route Table.

### Public Route Table

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

---

### Private Route Table

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | NAT Gateway |

---

# 🌐 Auto Assign Public IP

AWS allows automatic assignment of Public IP addresses.

Enable for:

- Web Servers
- Bastion Hosts

Disable for:

- Databases
- Backend Servers
- Internal Services

---

# 🏢 Example Production Architecture

```text
                    Internet
                        │
                 Internet Gateway
                        │
              ┌─────────┴─────────┐
              ▼                   ▼
      Public Subnet A      Public Subnet B
      Load Balancer         Bastion Host
              │
      ┌───────┴────────┐
      ▼                ▼
 Private Subnet A   Private Subnet B
 Application EC2    Application EC2
      │                │
      └────────┬───────┘
               ▼
          Database Subnet
              Amazon RDS
```

---

# 💻 Useful AWS CLI Commands

### List Subnets

```bash
aws ec2 describe-subnets
```

---

### Create a Subnet

```bash
aws ec2 create-subnet \
--vpc-id vpc-xxxxxxxx \
--cidr-block 10.0.1.0/24 \
--availability-zone ap-south-1a
```

---

### Modify Auto Assign Public IP

```bash
aws ec2 modify-subnet-attribute \
--subnet-id subnet-xxxxxxxx \
--map-public-ip-on-launch
```

---

### Delete a Subnet

```bash
aws ec2 delete-subnet \
--subnet-id subnet-xxxxxxxx
```

---

# 💡 Best Practices

✅ Separate Public and Private resources

✅ Use multiple Availability Zones

✅ Keep databases in Private Subnets

✅ Place Load Balancers in Public Subnets

✅ Plan CIDR ranges before deployment

✅ Use meaningful subnet names

✅ Enable Auto Public IP only where required

---

# 🌍 Common Use Cases

| Resource | Recommended Subnet |
|-----------|--------------------|
| Web Server | Public |
| Application Server | Private |
| Database | Private |
| Bastion Host | Public |
| NAT Gateway | Public |
| Load Balancer | Public |
| Redis Cache | Private |

---

# 📝 Key Takeaways

- A subnet is a smaller network inside a VPC.
- Public subnets have Internet access through an Internet Gateway.
- Private subnets do not have direct Internet access.
- Every subnet belongs to one Availability Zone.
- Route Tables determine whether a subnet is public or private.
- AWS reserves five IP addresses in every subnet.

---

# 📋 Summary

In this chapter, you learned:

- What is a Subnet?
- Public vs Private Subnets
- CIDR Planning
- Availability Zones
- Route Tables
- Public IP Assignment
- Production Architecture
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a subnet?
2. Why do we divide a VPC into subnets?
3. What is a Public Subnet?
4. What is a Private Subnet?
5. How many IP addresses does AWS reserve in each subnet?

---

## Intermediate

6. Explain how Route Tables determine subnet type.
7. Why should databases be placed in Private Subnets?
8. What is the relationship between Subnets and Availability Zones?
9. What is Auto Assign Public IP?
10. Can a subnet span multiple Availability Zones?

---

## Advanced

11. Design a subnet architecture for a highly available web application.
12. How would you plan CIDR blocks for a large enterprise?
13. Explain why NAT Gateway is required for Private Subnets.
14. What are common subnet design mistakes in AWS?

---

# 🎯 Practice Exercises

## Exercise 1

Create a VPC with CIDR:

```text
10.0.0.0/16
```

---

## Exercise 2

Create:

- Public Subnet A
- Public Subnet B
- Private Subnet A
- Private Subnet B

---

## Exercise 3

Associate Route Tables with each subnet.

---

## Exercise 4

Enable Auto Assign Public IP for the Public Subnet.

---

## Exercise 5

Launch:

- One EC2 instance in a Public Subnet
- One EC2 instance in a Private Subnet

Verify network connectivity.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-subnet-design.md
```

Include:

- VPC CIDR
- Subnet Layout
- Public vs Private Comparison
- Route Table Configuration
- Availability Zone Distribution
- Best Practices
- AWS CLI Commands

Commit it to Git:

```bash
git add .
git commit -m "Add AWS subnet architecture guide"
```

---

# 📚 Further Reading

- Amazon VPC User Guide
- Subnets in Amazon VPC
- Route Tables
- Internet Gateway
- NAT Gateway
- AWS Networking Best Practices

---

# 🚀 What's Next?

In **Chapter 09 – Internet Gateway & NAT Gateway**, you'll learn:

- 🌐 Internet Gateway (IGW)
- 🔄 NAT Gateway
- 📡 NAT Instance
- 🛣️ Route Tables
- Internet Connectivity Flow
- Public vs Private Routing
- High Availability Design
- AWS CLI Commands
- Best Practices
- Production Networking Architecture
