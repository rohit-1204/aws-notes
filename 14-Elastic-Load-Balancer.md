# AWS Notes
# Chapter 14 - Elastic Load Balancer (ELB)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 70–90 minutes
> 🛠️ **Practice Time:** 3–5 hours

---

# 📚 Table of Contents

1. What is Elastic Load Balancer?
2. Why Do We Need a Load Balancer?
3. How ELB Works
4. Types of Load Balancers
5. Application Load Balancer (ALB)
6. Network Load Balancer (NLB)
7. Gateway Load Balancer (GWLB)
8. Classic Load Balancer (CLB)
9. Target Groups
10. Health Checks
11. Cross-Zone Load Balancing
12. SSL/TLS Termination
13. Sticky Sessions
14. Path-Based & Host-Based Routing
15. ELB Architecture
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

- Understand Elastic Load Balancer
- Explain why load balancing is required
- Differentiate ALB, NLB, GWLB and CLB
- Configure Target Groups
- Understand Health Checks
- Build highly available AWS applications

---

# 📖 What is Elastic Load Balancer?

**Elastic Load Balancer (ELB)** is an AWS service that automatically distributes incoming traffic across multiple servers (targets).

Instead of sending all traffic to one server, ELB shares the load among healthy servers.

This improves:

- ⚡ Performance
- 🔒 Availability
- 📈 Scalability
- 🛡️ Fault Tolerance

---

# 💡 Why Do We Need a Load Balancer?

Imagine 10,000 users visiting your website.

Without a Load Balancer:

```text
Users
   │
   ▼
Single EC2
```

Problems:

- ❌ Server overload
- ❌ Downtime
- ❌ Slow response
- ❌ Single point of failure

---

With ELB:

```text
Users
   │
   ▼
Load Balancer
   │
 ┌─┴─────────────┐
 ▼               ▼
EC2-1         EC2-2
                 │
                 ▼
               EC2-3
```

Traffic is distributed automatically.

---

# 🧠 How ELB Works

Traffic Flow:

```text
Client
   │
   ▼
DNS
   │
   ▼
Elastic Load Balancer
   │
 ┌─┴───────────────┐
 ▼                 ▼
EC2 Instance    EC2 Instance
```

The ELB continuously checks server health and routes traffic only to healthy instances.

---

# 🌐 Types of AWS Load Balancers

AWS provides four types of Load Balancers.

| Load Balancer | Layer | Best For |
|---------------|-------|----------|
| Application Load Balancer (ALB) | Layer 7 | HTTP/HTTPS Applications |
| Network Load Balancer (NLB) | Layer 4 | TCP/UDP Applications |
| Gateway Load Balancer (GWLB) | Layer 3/4 | Virtual Appliances |
| Classic Load Balancer (CLB) | Legacy | Older Applications |

---

# 🚀 Application Load Balancer (ALB)

ALB works at **Layer 7 (Application Layer)**.

Supports:

- HTTP
- HTTPS
- WebSockets
- HTTP/2

Features:

- Path-based routing
- Host-based routing
- SSL termination
- Authentication
- Target groups

Example:

```text
example.com/api → API Server

example.com/images → Image Server
```

---

# ⚡ Network Load Balancer (NLB)

NLB works at **Layer 4 (Transport Layer)**.

Supports:

- TCP
- UDP
- TLS

Features:

- Ultra-low latency
- Millions of requests
- Static IP support
- High performance

Ideal for:

- Gaming
- Financial systems
- High-performance applications

---

# 🛡️ Gateway Load Balancer (GWLB)

GWLB is designed for virtual network appliances.

Examples:

- Firewalls
- IDS
- IPS
- Security Appliances

Traffic:

```text
Internet
    │
GWLB
    │
Firewall
    │
Application
```

---

# 📜 Classic Load Balancer (CLB)

Classic Load Balancer is the original AWS Load Balancer.

Supports:

- HTTP
- HTTPS
- TCP

Today:

⚠️ Not recommended for new applications.

Use ALB or NLB instead.

---

# 🎯 Target Groups

A **Target Group** contains backend resources.

Targets can be:

- 🖥️ EC2 Instances
- 📦 ECS Tasks
- ☸️ EKS Pods
- 🖧 IP Addresses
- ⚡ Lambda Functions (ALB)

Example:

```text
ALB
 │
 ▼
Target Group
 │
 ├── EC2-1
 ├── EC2-2
 └── EC2-3
```

---

# ❤️ Health Checks

ELB continuously checks whether targets are healthy.

Example:

```text
GET /health
```

Healthy:

✅ Requests sent

Unhealthy:

❌ Removed from traffic

---

Health Check Settings:

- Protocol
- Port
- Path
- Timeout
- Interval
- Healthy Threshold
- Unhealthy Threshold

---

# 🌍 Cross-Zone Load Balancing

Without Cross-Zone:

```text
AZ-A → EC2-A

AZ-B → EC2-B
```

Traffic may not be balanced evenly.

---

With Cross-Zone:

```text
            ELB
      ┌──────┴──────┐
      ▼             ▼
AZ-A EC2s      AZ-B EC2s
```

Traffic is evenly distributed across all Availability Zones.

---

# 🔒 SSL/TLS Termination

Instead of configuring SSL on every EC2 instance:

```text
Client (HTTPS)
      │
      ▼
ELB (Decrypts SSL)
      │
HTTP
      ▼
EC2
```

Benefits:

- Simplified certificate management
- Better performance
- Easier maintenance

---

# 🍪 Sticky Sessions

Sticky Sessions keep a user connected to the same backend server.

Example:

```text
User A → EC2-1

User A → EC2-1

User A → EC2-1
```

Useful for:

- Shopping carts
- Legacy web applications

---

# 🛣️ Path-Based Routing

Example:

```text
/app/*

→ Application Server
```

```text
/images/*

→ Image Server
```

```text
/api/*

→ API Server
```

One ALB can route traffic to multiple applications.

---

# 🌐 Host-Based Routing

Example:

```text
api.example.com

→ API Target Group
```

```text
shop.example.com

→ Shopping Target Group
```

```text
blog.example.com

→ Blog Target Group
```

---

# 🏗️ ELB Architecture

```text
                  Internet
                      │
                      ▼
               Route 53 (DNS)
                      │
                      ▼
          Application Load Balancer
              ┌────────┴────────┐
              ▼                 ▼
          Target Group      Target Group
              │                 │
        ┌─────┴─────┐     ┌─────┴─────┐
        ▼           ▼     ▼           ▼
      EC2-1      EC2-2   EC2-3      EC2-4
```

---

# 💻 Useful AWS CLI Commands

## List Load Balancers

```bash
aws elbv2 describe-load-balancers
```

---

## Create a Target Group

```bash
aws elbv2 create-target-group \
--name WebTG \
--protocol HTTP \
--port 80 \
--vpc-id vpc-xxxxxxxx
```

---

## Register Targets

```bash
aws elbv2 register-targets \
--target-group-arn <TARGET_GROUP_ARN> \
--targets Id=i-xxxxxxxx
```

---

## Create an Application Load Balancer

```bash
aws elbv2 create-load-balancer \
--name MyALB \
--subnets subnet-xxxx subnet-yyyy \
--security-groups sg-xxxxxxxx
```

---

## Create a Listener

```bash
aws elbv2 create-listener \
--load-balancer-arn <ALB_ARN> \
--protocol HTTP \
--port 80 \
--default-actions Type=forward,TargetGroupArn=<TARGET_GROUP_ARN>
```

---

# 💡 Best Practices

✅ Deploy Load Balancers across multiple Availability Zones.

✅ Enable Health Checks.

✅ Use HTTPS for production workloads.

✅ Enable Cross-Zone Load Balancing.

✅ Use Auto Scaling with ELB.

✅ Monitor using CloudWatch.

✅ Use ALB for web applications.

✅ Use NLB for high-performance TCP/UDP workloads.

---

# 🌍 Common Use Cases

| Scenario | Recommended Load Balancer |
|----------|---------------------------|
| Web Application | ALB |
| REST API | ALB |
| Microservices | ALB |
| Gaming Server | NLB |
| Banking Application | NLB |
| Firewall Appliance | GWLB |
| Legacy Application | CLB |

---

# 📝 Key Takeaways

- ELB distributes incoming traffic across multiple targets.
- Improves availability and fault tolerance.
- ALB operates at Layer 7.
- NLB operates at Layer 4.
- GWLB is designed for virtual appliances.
- Health Checks ensure only healthy targets receive traffic.
- Target Groups contain backend resources.
- Cross-Zone Load Balancing improves traffic distribution.

---

# 📋 Summary

In this chapter, you learned:

- Elastic Load Balancer
- Application Load Balancer
- Network Load Balancer
- Gateway Load Balancer
- Classic Load Balancer
- Target Groups
- Health Checks
- SSL Termination
- Sticky Sessions
- Path-Based Routing
- Host-Based Routing
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is an Elastic Load Balancer?
2. Why do we use a Load Balancer?
3. Name the four types of AWS Load Balancers.
4. What is a Target Group?
5. What is a Health Check?

---

## Intermediate

6. Differentiate ALB and NLB.
7. What is SSL Termination?
8. Explain Sticky Sessions.
9. What is Cross-Zone Load Balancing?
10. Explain Path-Based Routing.

---

## Advanced

11. Design a highly available web application using ALB.
12. Explain how Health Checks improve reliability.
13. When would you choose NLB instead of ALB?
14. Explain Host-Based Routing with an example.
15. How would you troubleshoot unhealthy targets behind an ALB?

---

# 🎯 Practice Exercises

## Exercise 1

Create an Application Load Balancer.

---

## Exercise 2

Create a Target Group.

---

## Exercise 3

Launch two EC2 instances and register them with the Target Group.

---

## Exercise 4

Create an HTTP Listener on port **80**.

---

## Exercise 5

Stop one EC2 instance and verify that ELB routes traffic only to the healthy instance.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-elb-guide.md
```

Include:

- ELB Overview
- Types of Load Balancers
- ALB vs NLB
- Target Groups
- Health Checks
- Cross-Zone Load Balancing
- SSL Termination
- Path-Based Routing
- Host-Based Routing
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Elastic Load Balancer guide"
```

---

# 📚 Further Reading

- AWS Elastic Load Balancing Documentation
- Application Load Balancer User Guide
- Network Load Balancer User Guide
- Gateway Load Balancer Documentation
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 15 – Auto Scaling Groups (ASG)**, you'll learn:

- 📈 What is Auto Scaling?
- 👥 Auto Scaling Groups (ASG)
- 🚀 Launch Templates
- 📊 Scaling Policies
- ❤️ Health Checks
- 🎯 Desired, Minimum & Maximum Capacity
- ⚖️ Dynamic vs Predictive Scaling
- 🔄 ELB Integration
- 💻 AWS CLI Commands
- 🔒 Best Practices
