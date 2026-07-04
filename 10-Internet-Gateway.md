# AWS Notes
# Chapter 10 - Internet Gateway (IGW)

> 📘 **Level:** Beginner
> ⏱️ **Estimated Reading Time:** 45–60 minutes
> 🛠️ **Practice Time:** 2–3 hours

---

# 📚 Table of Contents

1. What is an Internet Gateway?
2. Why Do We Need an Internet Gateway?
3. How Internet Gateway Works
4. Internet Gateway Architecture
5. Public vs Private Connectivity
6. Attaching an Internet Gateway
7. Route Tables and Internet Gateway
8. Public IP Addresses
9. Internet Gateway vs NAT Gateway
10. AWS CLI Commands
11. Best Practices
12. Common Use Cases
13. Summary
14. Interview Questions
15. Practice Exercises
16. Mini Project
17. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand what an Internet Gateway (IGW) is
- Explain how Internet connectivity works in AWS
- Attach an Internet Gateway to a VPC
- Configure Route Tables for public access
- Launch publicly accessible EC2 instances
- Differentiate between Internet Gateway and NAT Gateway
- Design secure public network architectures

---

# 📖 What is an Internet Gateway?

An **Internet Gateway (IGW)** is an AWS-managed networking component that enables communication between resources in your **Amazon VPC** and the public Internet.

Without an Internet Gateway, resources inside a VPC **cannot communicate with the Internet**.

An Internet Gateway is:

- 🌐 Highly Available
- ⚡ Horizontally Scalable
- 🔒 Fully Managed by AWS
- 🚀 Automatically Redundant

---

# 💡 Why Do We Need an Internet Gateway?

An Internet Gateway allows AWS resources to:

- 🌍 Access websites
- 📦 Download software updates
- ☁️ Communicate with external APIs
- 🌐 Host public websites
- 🔄 Receive incoming Internet traffic

Without an IGW:

- ❌ No Internet Access
- ❌ No Public Website
- ❌ No SSH from the Internet

---

# 🧠 How Internet Gateway Works

The communication flow is:

```text
EC2 Instance
      │
      ▼
Public Subnet
      │
      ▼
Route Table
      │
      ▼
Internet Gateway
      │
      ▼
Internet
```

The Route Table tells AWS to send Internet-bound traffic through the Internet Gateway.

---

# 🏗️ Internet Gateway Architecture

```text
                 Internet
                     │
                     ▼
          Internet Gateway (IGW)
                     │
             Public Route Table
                     │
          Public Subnet (EC2)
                     │
              Web Application
```

---

# 🌍 Public vs Private Connectivity

## 🌐 Public Subnet

Requirements:

- Internet Gateway attached
- Route to `0.0.0.0/0`
- Public IP or Elastic IP

Example:

```text
Internet
     │
IGW
     │
Public Route Table
     │
Public EC2
```

---

## 🔐 Private Subnet

Private subnets:

- Do not use Internet Gateway directly
- Use a NAT Gateway for outbound Internet access
- Cannot receive incoming Internet traffic

Example:

```text
Private EC2
      │
Private Route Table
      │
NAT Gateway
      │
Internet
```

---

# 🔗 Attaching an Internet Gateway

Steps:

1. Open **AWS VPC Console**
2. Select **Internet Gateways**
3. Click **Create Internet Gateway**
4. Provide a name
5. Click **Create**
6. Select **Attach to VPC**
7. Choose your VPC

Once attached, configure the Route Table.

---

# 🛣️ Configuring Route Tables

To make a subnet public, add the following route:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | Internet Gateway |

Example:

```text
Destination : 0.0.0.0/0
Target      : igw-xxxxxxxx
```

---

# 🌐 Public IP Addresses

An Internet Gateway alone is **not enough**.

The EC2 instance must also have:

- ✅ Public IPv4 Address
or
- ✅ Elastic IP Address

Without a public IP, the Internet cannot reach the instance.

---

# 📌 Conditions for Internet Access

For an EC2 instance to access the Internet:

✅ Internet Gateway attached to the VPC

✅ Route Table contains:

```text
0.0.0.0/0 → Internet Gateway
```

✅ Instance has a Public IP

✅ Security Group allows required traffic

✅ Network ACL allows the traffic

---

# ⚖️ Internet Gateway vs NAT Gateway

| Internet Gateway | NAT Gateway |
|------------------|-------------|
| Used by Public Subnets | Used by Private Subnets |
| Allows inbound & outbound traffic | Outbound traffic only |
| Requires Public IP on EC2 | No Public IP required |
| Public-facing | Private networking |

---

# 🏢 Production Architecture

```text
                    Internet
                        │
                Internet Gateway
                        │
                Public Route Table
                        │
        ┌───────────────┴──────────────┐
        ▼                              ▼
 Public Subnet A                 Public Subnet B
  Load Balancer                  Bastion Host
        │
        ▼
 Application Servers
        │
        ▼
 Private Route Table
        │
   NAT Gateway
        │
     Internet
```

---

# 🔒 Security Considerations

Although the Internet Gateway enables connectivity, security is controlled by:

- 🔐 Security Groups
- 🛡️ Network ACLs
- 🔑 IAM Policies

Always expose only the required ports.

Example:

| Port | Purpose |
|------|----------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |

Avoid opening unnecessary ports.

---

# 💻 Useful AWS CLI Commands

## Create an Internet Gateway

```bash
aws ec2 create-internet-gateway
```

---

## List Internet Gateways

```bash
aws ec2 describe-internet-gateways
```

---

## Attach an Internet Gateway

```bash
aws ec2 attach-internet-gateway \
--internet-gateway-id igw-xxxxxxxx \
--vpc-id vpc-xxxxxxxx
```

---

## Detach an Internet Gateway

```bash
aws ec2 detach-internet-gateway \
--internet-gateway-id igw-xxxxxxxx \
--vpc-id vpc-xxxxxxxx
```

---

## Delete an Internet Gateway

```bash
aws ec2 delete-internet-gateway \
--internet-gateway-id igw-xxxxxxxx
```

---

# 💡 Best Practices

✅ Use an Internet Gateway only for Public Subnets.

✅ Place databases in Private Subnets.

✅ Use Security Groups with least privilege.

✅ Enable HTTPS instead of HTTP whenever possible.

✅ Use Elastic IPs only when necessary.

✅ Monitor public resources using CloudWatch and VPC Flow Logs.

---

# 🌍 Common Use Cases

| Scenario | Internet Gateway Required? |
|-----------|----------------------------|
| Public Website | ✅ Yes |
| Web Server | ✅ Yes |
| Bastion Host | ✅ Yes |
| Application Load Balancer | ✅ Yes |
| Database Server | ❌ No |
| Backend API | ❌ Usually No |

---

# 📝 Key Takeaways

- An Internet Gateway connects a VPC to the Internet.
- It is highly available and managed by AWS.
- Public Subnets require an Internet Gateway.
- A Route Table must contain a route to the IGW.
- EC2 instances also require a Public IP for Internet access.
- Security Groups and NACLs still control network access.

---

# 📋 Summary

In this chapter, you learned:

- Internet Gateway
- Public Internet Access
- Route Table Configuration
- Public IP Addresses
- Internet Gateway vs NAT Gateway
- AWS CLI Commands
- Best Practices
- Production Architecture

---

# ❓ Interview Questions

## Beginner

1. What is an Internet Gateway?
2. Why is an Internet Gateway required?
3. Can an EC2 instance access the Internet without an IGW?
4. What Route Table entry enables Internet access?
5. Does an Internet Gateway assign Public IP addresses?

---

## Intermediate

6. Explain how Internet traffic reaches an EC2 instance.
7. What additional requirements are needed besides an IGW?
8. Differentiate between Public and Private Subnets.
9. Explain the relationship between Route Tables and IGWs.
10. What happens if an EC2 instance has no Public IP?

---

## Advanced

11. Design a highly available public network architecture.
12. Explain Internet Gateway packet flow.
13. How would you secure Internet-facing EC2 instances?
14. Compare Internet Gateway and NAT Gateway in production environments.

---

# 🎯 Practice Exercises

## Exercise 1

Create a new Internet Gateway.

---

## Exercise 2

Attach it to your VPC.

---

## Exercise 3

Update the Public Route Table:

```text
0.0.0.0/0 → Internet Gateway
```

---

## Exercise 4

Launch an EC2 instance with a Public IP.

Verify Internet connectivity using:

```bash
ping google.com
```

---

## Exercise 5

Access the EC2 instance using SSH from your local machine.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-internet-gateway-guide.md
```

Include:

- Internet Gateway Overview
- Architecture Diagram
- Internet Traffic Flow
- Route Table Configuration
- Public IP Requirements
- Internet Gateway vs NAT Gateway
- AWS CLI Commands
- Security Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Internet Gateway documentation"
```

---

# 📚 Further Reading

- Amazon VPC Internet Gateway Documentation
- Amazon VPC User Guide
- AWS Networking Best Practices
- Security Groups Documentation
- VPC Route Tables Guide

---

# 🚀 What's Next?

In **Chapter 11 – NAT Gateway**, you'll learn:

- 🌐 What is a NAT Gateway?
- 🔄 Outbound Internet Access for Private Subnets
- 🖥️ NAT Gateway vs NAT Instance
- 🛣️ Route Table Configuration
- 💰 NAT Gateway Pricing
- 🏗️ High Availability Design
- 💻 AWS CLI Commands
- 🔒 Security Best Practices
