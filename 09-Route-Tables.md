# AWS Notes
# Chapter 09 - Route Tables

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 45–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is a Route Table?
2. Why Do We Need Route Tables?
3. How Routing Works
4. Components of a Route Table
5. Local Route
6. Internet Gateway Route
7. NAT Gateway Route
8. Route Table Association
9. Main Route Table
10. Custom Route Tables
11. Route Priority
12. Production Architecture
13. AWS CLI Commands
14. Best Practices
15. Common Use Cases
16. Summary
17. Interview Questions
18. Practice Exercises
19. Mini Project
20. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Route Tables
- Configure routing inside a VPC
- Associate Route Tables with Subnets
- Configure Internet and NAT Gateway routes
- Understand Local Routing
- Build secure AWS network architectures

---

# 📖 What is a Route Table?

A **Route Table** is a set of rules (routes) that determines where network traffic from a subnet should be sent.

Every subnet in an Amazon VPC **must be associated with a Route Table**.

Think of a Route Table as a **GPS for your network traffic**.

---

# 💡 Why Do We Need Route Tables?

Route Tables help:

- 🌐 Send traffic to the Internet
- 🔄 Connect private resources using NAT Gateway
- 🔗 Connect VPCs together
- 🛡️ Control network traffic
- 🏢 Build secure network architectures

Without Route Tables, AWS resources would not know where to send network packets.

---

# 🧠 How Routing Works

When an EC2 instance sends a packet:

1. The packet reaches the subnet.
2. The subnet checks its associated Route Table.
3. AWS compares the destination IP with available routes.
4. The most specific matching route is selected.
5. Traffic is forwarded to the target.

---

# 🏗️ Route Table Architecture

```text
                 EC2 Instance
                      │
                      ▼
              Route Table Lookup
                      │
        ┌─────────────┼─────────────┐
        │             │             │
        ▼             ▼             ▼
     Local         Internet      NAT Gateway
```

---

# 📦 Components of a Route Table

Each route contains:

| Component | Description |
|------------|-------------|
| Destination | IP range (CIDR Block) |
| Target | Where traffic should go |

Example:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

---

# 🏠 Local Route

Every VPC automatically contains a **Local Route**.

Example:

```text
Destination : 10.0.0.0/16
Target      : Local
```

Purpose:

Allows communication between subnets inside the same VPC.

Example:

```text
Public EC2
     │
     ▼
Private Database
```

No Internet is required.

---

# 🌐 Internet Gateway Route

To make a subnet public, add:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | Internet Gateway |

Example:

```text
Internet
    │
Internet Gateway
    │
Route Table
    │
Public Subnet
```

Resources in the subnet can communicate with the Internet.

---

# 🔄 NAT Gateway Route

Private subnets cannot access the Internet directly.

Instead, configure:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | NAT Gateway |

Example:

```text
Private EC2
      │
      ▼
Route Table
      │
      ▼
NAT Gateway
      │
      ▼
Internet
```

This allows outbound Internet access while blocking inbound connections.

---

# 🔗 Route Table Association

Each subnet is associated with exactly one Route Table.

A single Route Table can be associated with multiple subnets.

Example:

```text
Route Table A
     │
 ┌───┴─────┐
 ▼         ▼
Subnet1  Subnet2
```

---

# 🏠 Main Route Table

Every VPC has a **Main Route Table**.

Characteristics:

- Created automatically
- Associated with new subnets by default
- Can be replaced with a custom Main Route Table

---

# 🛠️ Custom Route Tables

For production environments, create separate Route Tables.

Example:

| Route Table | Used For |
|--------------|----------|
| Public RT | Public Subnets |
| Private RT | Private Subnets |
| Database RT | Database Subnets |

Benefits:

- Better organization
- Improved security
- Easier troubleshooting

---

# 🎯 Longest Prefix Match

AWS uses the **Longest Prefix Match** rule.

Example:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 10.0.1.0/24 | Firewall |
| 0.0.0.0/0 | Internet Gateway |

Traffic to:

```
10.0.1.25
```

Uses:

```
10.0.1.0/24
```

because it is the most specific route.

---

# 🏢 Production Route Table Design

```text
                    Internet
                        │
                Internet Gateway
                        │
               Public Route Table
                        │
              Public Subnet (ALB)
                        │
                Application EC2
                        │
               Private Route Table
                        │
                  NAT Gateway
                        │
                     Internet
```

---

# 🔐 Route Tables and Security

Remember:

- Route Tables decide **where** traffic goes.
- Security Groups decide **who** can access an instance.
- Network ACLs decide **what traffic** is allowed at the subnet level.

All three work together to secure your AWS network.

---

# 💻 Useful AWS CLI Commands

## List Route Tables

```bash
aws ec2 describe-route-tables
```

---

## Create a Route Table

```bash
aws ec2 create-route-table \
--vpc-id vpc-xxxxxxxx
```

---

## Create a Route

```bash
aws ec2 create-route \
--route-table-id rtb-xxxxxxxx \
--destination-cidr-block 0.0.0.0/0 \
--gateway-id igw-xxxxxxxx
```

---

## Associate a Route Table

```bash
aws ec2 associate-route-table \
--route-table-id rtb-xxxxxxxx \
--subnet-id subnet-xxxxxxxx
```

---

## Delete a Route

```bash
aws ec2 delete-route \
--route-table-id rtb-xxxxxxxx \
--destination-cidr-block 0.0.0.0/0
```

---

# 💡 Best Practices

✅ Keep separate Route Tables for Public and Private Subnets.

✅ Use descriptive names.

✅ Avoid unnecessary routes.

✅ Use NAT Gateway for private workloads.

✅ Review routing regularly.

✅ Follow the principle of least privilege.

---

# 🌍 Common Use Cases

| Scenario | Route Target |
|-----------|--------------|
| Public Website | Internet Gateway |
| Private Server Updates | NAT Gateway |
| Internal Communication | Local Route |
| VPC Connectivity | VPC Peering |
| Hybrid Cloud | Virtual Private Gateway |

---

# 📝 Key Takeaways

- Every subnet requires a Route Table.
- Route Tables determine packet destinations.
- Public Subnets require an Internet Gateway route.
- Private Subnets typically use a NAT Gateway route.
- Every VPC contains a Main Route Table.
- AWS selects the most specific matching route.

---

# 📋 Summary

In this chapter, you learned:

- Route Tables
- Routing Process
- Local Route
- Internet Gateway Route
- NAT Gateway Route
- Route Associations
- Main vs Custom Route Tables
- Route Priority
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Route Table?
2. Why is a Route Table required?
3. What is a Local Route?
4. What is the default route (0.0.0.0/0)?
5. Can multiple subnets share one Route Table?

---

## Intermediate

6. Explain Public and Private Route Tables.
7. What is the Main Route Table?
8. How does AWS choose between multiple matching routes?
9. Why do private subnets use NAT Gateway?
10. Can a subnet have multiple Route Tables?

---

## Advanced

11. Design Route Tables for a highly available web application.
12. Explain Longest Prefix Match with an example.
13. How would you isolate database traffic using Route Tables?
14. How would you troubleshoot routing issues in AWS?

---

# 🎯 Practice Exercises

## Exercise 1

Create a custom Route Table.

---

## Exercise 2

Associate the Route Table with a Public Subnet.

---

## Exercise 3

Add a route:

```text
0.0.0.0/0 → Internet Gateway
```

---

## Exercise 4

Create a Private Route Table using a NAT Gateway.

---

## Exercise 5

Launch EC2 instances in both Public and Private Subnets and verify network connectivity.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-route-table-design.md
```

Include:

- VPC Architecture
- Public Route Table
- Private Route Table
- Local Routes
- Internet Gateway Route
- NAT Gateway Route
- Route Table Associations
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add AWS Route Tables guide"
```

---

# 📚 Further Reading

- Amazon VPC Route Tables
- Internet Gateway Documentation
- NAT Gateway Documentation
- VPC Networking Best Practices
- AWS CLI EC2 Reference

---

# 🚀 What's Next?

In **Chapter 10 – Internet Gateway & NAT Gateway**, you'll learn:

- 🌐 Internet Gateway (IGW)
- 🔄 NAT Gateway
- 🖥️ NAT Instance
- 📡 Outbound vs Inbound Internet Access
- 🛣️ Routing with IGW and NAT
- 🔒 Secure Internet Connectivity
- 💻 AWS CLI Commands
- 🏗️ Production Network Design
```
