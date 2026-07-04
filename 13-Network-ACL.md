# AWS Notes
# Chapter 13 - Network Access Control Lists (Network ACLs)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is a Network ACL?
2. Why Do We Need Network ACLs?
3. How Network ACLs Work
4. Stateless Firewall
5. Inbound Rules
6. Outbound Rules
7. Rule Evaluation
8. Default vs Custom NACL
9. Network ACL Architecture
10. Common Rule Examples
11. Network ACL vs Security Group
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

- Understand what a Network ACL is
- Configure inbound and outbound rules
- Explain stateless firewalls
- Secure subnets using NACLs
- Differentiate Security Groups and Network ACLs
- Apply AWS networking best practices

---

# 📖 What is a Network ACL?

A **Network Access Control List (Network ACL or NACL)** is an optional **subnet-level firewall** that controls inbound and outbound network traffic.

Unlike Security Groups, Network ACLs are associated with **subnets**, not individual instances.

They provide an additional layer of security for your VPC.

---

# 💡 Why Do We Need Network ACLs?

Network ACLs help:

- 🛡️ Protect entire subnets
- 🚫 Block malicious IP addresses
- 🌐 Control network traffic
- 🔒 Add another security layer
- 📜 Meet compliance requirements

Think of a Network ACL as a security checkpoint at the entrance of a subnet.

---

# 🧠 How Network ACLs Work

Traffic Flow:

```text
Internet
     │
     ▼
Internet Gateway
     │
     ▼
Network ACL
     │
     ▼
Security Group
     │
     ▼
EC2 Instance
```

Traffic must pass through both the Network ACL and the Security Group.

---

# ⚡ Network ACLs are Stateless

A Network ACL is a **Stateless Firewall**.

This means:

- Incoming traffic is checked.
- Outgoing traffic is checked separately.

If you allow inbound traffic, you must also allow the corresponding outbound traffic.

Example:

```text
Laptop
   │ SSH
   ▼
Inbound Rule ✔
   │
EC2 Instance
   │
Outbound Rule ✔
   ▼
Laptop
```

Both rules are required.

---

# 🚪 Inbound Rules

Inbound Rules control traffic entering the subnet.

Example:

| Rule | Protocol | Port | Source | Action |
|------|----------|------|---------|--------|
| 100 | TCP | 22 | Your IP | Allow |
| 110 | TCP | 80 | 0.0.0.0/0 | Allow |
| 120 | TCP | 443 | 0.0.0.0/0 | Allow |
| * | All | All | All | Deny |

---

# 🚀 Outbound Rules

Outbound Rules control traffic leaving the subnet.

Example:

| Rule | Protocol | Port | Destination | Action |
|------|----------|------|-------------|--------|
| 100 | All | All | 0.0.0.0/0 | Allow |
| * | All | All | All | Deny |

---

# 🔢 Rule Evaluation

Rules are processed from the **lowest rule number** to the highest.

Example:

```text
Rule 100 → Allow SSH
Rule 110 → Allow HTTP
Rule 120 → Allow HTTPS
Rule *   → Deny Everything
```

The **first matching rule wins**.

---

# 📋 Default Network ACL

Every VPC comes with a **Default Network ACL**.

Features:

- ✅ Allows all inbound traffic
- ✅ Allows all outbound traffic
- ✅ Can be modified
- ✅ Automatically associated with new subnets

---

# 🛡️ Custom Network ACL

A Custom Network ACL starts with:

- ❌ No inbound rules (except deny)
- ❌ No outbound rules (except deny)

You must explicitly add Allow rules.

---

# 🏗️ Network ACL Architecture

```text
                Internet
                    │
                    ▼
            Internet Gateway
                    │
            ┌──────────────┐
            │ Network ACL  │
            └──────────────┘
                    │
           Public Subnet
                    │
           ┌──────────────┐
           │Security Group│
           └──────────────┘
                    │
                EC2 Instance
```

---

# 🌐 Common Rule Examples

## Web Server Subnet

| Rule | Port | Action |
|------|------|--------|
| 100 | 80 | Allow |
| 110 | 443 | Allow |
| 120 | 22 | Allow |
| * | All | Deny |

---

## Database Subnet

| Rule | Port | Source | Action |
|------|------|---------|--------|
| 100 | 3306 | Application Subnet | Allow |
| * | All | All | Deny |

---

## Blocking an IP Address

Example:

```text
Rule 90
Source: 203.0.113.10/32
Action: Deny
```

This blocks traffic from that specific IP.

---

# ⚖️ Network ACL vs Security Group

| Network ACL | Security Group |
|--------------|---------------|
| Subnet Level | Instance Level |
| Stateless | Stateful |
| Allow & Deny Rules | Allow Rules Only |
| Rule Number Priority | No Rule Numbers |
| One NACL per Subnet | Multiple SGs per Instance |

---

# 🚫 Common Mistakes

❌ Forgetting outbound rules.

Since NACLs are stateless, responses also require explicit outbound rules.

---

❌ Incorrect rule order.

Example:

```text
100 Deny All
110 Allow HTTP
```

HTTP will never be allowed because Rule 100 matches first.

---

❌ Opening unnecessary ports.

Allow only required services.

---

# 💻 Useful AWS CLI Commands

## List Network ACLs

```bash
aws ec2 describe-network-acls
```

---

## Create a Network ACL

```bash
aws ec2 create-network-acl \
--vpc-id vpc-xxxxxxxx
```

---

## Create an Inbound Rule

```bash
aws ec2 create-network-acl-entry \
--network-acl-id acl-xxxxxxxx \
--rule-number 100 \
--protocol tcp \
--port-range From=80,To=80 \
--cidr-block 0.0.0.0/0 \
--rule-action allow \
--ingress
```

---

## Create an Outbound Rule

```bash
aws ec2 create-network-acl-entry \
--network-acl-id acl-xxxxxxxx \
--rule-number 100 \
--protocol -1 \
--cidr-block 0.0.0.0/0 \
--rule-action allow \
--egress
```

---

## Delete a Rule

```bash
aws ec2 delete-network-acl-entry \
--network-acl-id acl-xxxxxxxx \
--rule-number 100 \
--ingress
```

---

# 💡 Best Practices

✅ Use Security Groups as the primary firewall.

✅ Use Network ACLs as an additional security layer.

✅ Block known malicious IP ranges.

✅ Keep rule numbers organized (100, 110, 120...).

✅ Allow ephemeral ports when required.

✅ Test rules before deploying to production.

---

# 🌍 Common Use Cases

| Scenario | Network ACL |
|----------|-------------|
| Block malicious IPs | ✅ |
| Secure Public Subnet | ✅ |
| Secure Private Subnet | ✅ |
| Compliance Requirements | ✅ |
| Extra Layer of Security | ✅ |

---

# 📝 Key Takeaways

- Network ACLs protect **subnets**.
- They are **stateless** firewalls.
- Both inbound and outbound rules are required.
- Rules are evaluated in ascending order.
- NACLs support both **Allow** and **Deny** rules.
- They complement Security Groups.

---

# 📋 Summary

In this chapter, you learned:

- Network ACLs
- Stateless Firewall
- Inbound Rules
- Outbound Rules
- Rule Evaluation
- Default vs Custom NACL
- NACL vs Security Groups
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is a Network ACL?
2. At what level does a Network ACL operate?
3. Are Network ACLs stateful or stateless?
4. Can Network ACLs deny traffic?
5. What is the default action if no rule matches?

---

## Intermediate

6. Explain how rule evaluation works.
7. Differentiate Security Groups and Network ACLs.
8. Why are outbound rules required?
9. What is the difference between the Default and Custom NACL?
10. How do you block a specific IP using a Network ACL?

---

## Advanced

11. Design Network ACL rules for a three-tier application.
12. Explain packet flow through a VPC using NACLs and Security Groups.
13. How would you troubleshoot blocked traffic caused by a Network ACL?
14. Why should Network ACLs not replace Security Groups?

---

# 🎯 Practice Exercises

## Exercise 1

Create a Custom Network ACL.

---

## Exercise 2

Add inbound rules for:

- SSH (22)
- HTTP (80)
- HTTPS (443)

---

## Exercise 3

Add outbound rules allowing Internet access.

---

## Exercise 4

Associate the Network ACL with a Public Subnet.

---

## Exercise 5

Block a specific IP address and verify access is denied.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-network-acl-guide.md
```

Include:

- Network ACL Overview
- Stateless Firewall
- Architecture Diagram
- Inbound Rules
- Outbound Rules
- Rule Evaluation
- Default vs Custom NACL
- NACL vs Security Groups
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add AWS Network ACL guide"
```

---

# 📚 Further Reading

- AWS Network ACL Documentation
- Amazon VPC User Guide
- AWS Security Best Practices
- AWS Well-Architected Framework
- Amazon EC2 Networking Guide

---

# 🚀 What's Next?

In **Chapter 14 – Elastic Load Balancer (ELB)**, you'll learn:

- ⚖️ What is Load Balancing?
- 🌐 Types of AWS Load Balancers
- 🚀 Application Load Balancer (ALB)
- 🔌 Network Load Balancer (NLB)
- ☁️ Gateway Load Balancer (GWLB)
- ❤️ Health Checks
- 🎯 Target Groups
- 🔄 High Availability
- 💻 AWS CLI Commands
- 🔒 Best Practices
