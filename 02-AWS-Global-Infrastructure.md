# AWS Notes
# Chapter 02 - AWS Global Infrastructure

> **Level:** Beginner
> **Estimated Reading Time:** 45–60 minutes
> **Practice Time:** 1–2 hours

---

# Table of Contents

1. What is AWS Global Infrastructure?
2. Why Global Infrastructure Matters
3. AWS Regions
4. Availability Zones (AZs)
5. AWS Data Centers
6. Edge Locations
7. Regional Edge Caches
8. Local Zones
9. Wavelength Zones
10. AWS Outposts
11. Choosing the Right AWS Region
12. High Availability
13. Fault Tolerance
14. Disaster Recovery
15. Global Services vs Regional Services
16. AWS Infrastructure Architecture
17. Best Practices
18. Summary
19. Interview Questions
20. Practice Exercises
21. Mini Project
22. Further Reading

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand AWS Global Infrastructure
- Explain Regions and Availability Zones
- Differentiate Edge Locations, Local Zones, and Wavelength Zones
- Choose the right AWS Region
- Design highly available architectures
- Understand disaster recovery basics

---

# What is AWS Global Infrastructure?

AWS Global Infrastructure is the worldwide network of physical infrastructure that powers AWS services.

It consists of:

- Regions
- Availability Zones (AZs)
- Data Centers
- Edge Locations
- Regional Edge Caches
- Local Zones
- Wavelength Zones
- AWS Outposts

These components work together to deliver secure, reliable, and low-latency cloud services.

---

# AWS Global Infrastructure Overview

```text
                     AWS Global Infrastructure
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
     Regions             Edge Locations         AWS Outposts
        │
        ▼
Availability Zones (AZs)
        │
        ▼
   Data Centers
```

---

# Why Global Infrastructure Matters

AWS Global Infrastructure provides:

- High Availability
- Fault Tolerance
- Low Latency
- Disaster Recovery
- Scalability
- Global Application Deployment
- Data Residency Options

---

# What is an AWS Region?

A Region is a physical geographic location where AWS operates cloud infrastructure.

Each Region contains multiple Availability Zones.

Examples:

| Region Name | Code |
|-------------|------|
| US East (N. Virginia) | us-east-1 |
| US West (Oregon) | us-west-2 |
| Europe (Frankfurt) | eu-central-1 |
| Asia Pacific (Mumbai) | ap-south-1 |
| Asia Pacific (Singapore) | ap-southeast-1 |

---

# Region Architecture

```text
AWS Region
    │
    ├──────── AZ-A
    ├──────── AZ-B
    ├──────── AZ-C
    └──────── AZ-D
```

Each Region is isolated from every other Region.

---

# Why Multiple Regions?

Using multiple Regions provides:

- Better performance for global users
- Compliance with local regulations
- Disaster recovery
- Business continuity

---

# What is an Availability Zone (AZ)?

An Availability Zone (AZ) is one or more physically separate data centers within an AWS Region.

Each AZ has:

- Independent power
- Independent cooling
- Independent networking

They are connected using high-speed private fiber networks.

---

# Availability Zone Architecture

```text
Region (Mumbai)

├── AZ-A
│     ├── Data Center 1
│     └── Data Center 2
│
├── AZ-B
│     ├── Data Center 3
│     └── Data Center 4
│
└── AZ-C
      ├── Data Center 5
      └── Data Center 6
```

---

# Benefits of Multiple AZs

Deploying resources across multiple AZs helps achieve:

- High Availability
- Automatic Failover
- Fault Isolation
- Better Reliability

Example:

```text
        Load Balancer
          /      \
         /        \
    EC2 (AZ-A)  EC2 (AZ-B)
```

If one AZ becomes unavailable, traffic is routed to the healthy AZ.

---

# What are AWS Data Centers?

Data Centers are physical facilities containing:

- Servers
- Storage
- Networking equipment
- Cooling systems
- Backup power
- Physical security

AWS manages all hardware inside these facilities.

Customers never access them directly.

---

# Edge Locations

Edge Locations are AWS sites that cache and deliver content closer to users.

Used primarily by:

- Amazon CloudFront
- Route 53
- AWS Shield
- AWS Global Accelerator

Benefits:

- Faster content delivery
- Reduced latency
- Improved user experience

---

# Edge Location Architecture

```text
User
   │
   ▼
Edge Location
   │
   ▼
AWS Region
```

---

# Regional Edge Caches

Regional Edge Caches sit between Edge Locations and AWS Regions.

Benefits:

- Larger cache size
- Improved cache hit ratio
- Reduced latency
- Faster content retrieval

---

# Local Zones

Local Zones extend AWS infrastructure closer to large metropolitan areas.

Benefits:

- Ultra-low latency
- Ideal for:
  - Gaming
  - Media production
  - Real-time analytics
  - Machine Learning

Example:

```
Mumbai Region
      │
      ▼
Local Zone (Near users)
```

---

# Wavelength Zones

Wavelength Zones bring AWS services into 5G networks.

Designed for applications requiring extremely low latency.

Examples:

- AR/VR
- IoT
- Smart Cities
- Autonomous Vehicles
- Real-time Video Processing

---

# AWS Outposts

AWS Outposts extend AWS infrastructure into your own data center.

Useful when applications must remain on-premises due to:

- Compliance
- Regulatory requirements
- Low latency
- Hybrid cloud architectures

---

# AWS Infrastructure Components Comparison

| Component | Purpose |
|-----------|---------|
| Region | Geographic location |
| Availability Zone | Isolated data centers |
| Data Center | Physical hardware |
| Edge Location | Content delivery |
| Regional Edge Cache | Larger cache layer |
| Local Zone | Low-latency compute |
| Wavelength Zone | 5G edge computing |
| Outposts | AWS on-premises |

---

# Choosing the Right AWS Region

Consider:

- Distance from users
- Service availability
- Pricing
- Compliance requirements
- Disaster recovery strategy
- Latency

Example:

Users in India generally choose:

```
Asia Pacific (Mumbai)
```

---

# High Availability

High Availability (HA) ensures applications remain accessible even if part of the infrastructure fails.

Typical HA architecture:

```text
Internet
     │
     ▼
Load Balancer
   /       \
EC2(AZ-A) EC2(AZ-B)
```

If one instance or AZ fails, traffic is automatically routed to healthy resources.

---

# Fault Tolerance

Fault Tolerance allows systems to continue operating even during failures.

Methods include:

- Multiple Availability Zones
- Auto Scaling
- Elastic Load Balancer
- Multi-AZ Databases

---

# Disaster Recovery (DR)

Disaster Recovery protects applications from major failures such as Region outages.

Common AWS DR strategies:

- Backup & Restore
- Pilot Light
- Warm Standby
- Multi-Region Active-Active

---

# Global vs Regional AWS Services

| Global Services | Regional Services |
|-----------------|------------------|
| IAM | EC2 |
| Route 53 | VPC |
| CloudFront | RDS |
| Organizations | Lambda |
| WAF | EKS |

Global services are available across all Regions, while regional services must be created in a specific Region.

---

# Best Practices

✔ Deploy across multiple Availability Zones.

✔ Choose the Region closest to your users.

✔ Use CloudFront for global content delivery.

✔ Design for failure.

✔ Use Auto Scaling and Load Balancers.

✔ Consider compliance and data residency requirements.

---

# Key Takeaways

- AWS operates a global cloud infrastructure.
- Regions contain multiple Availability Zones.
- Availability Zones contain one or more Data Centers.
- Edge Locations improve content delivery speed.
- Local Zones and Wavelength Zones reduce latency.
- Outposts enable hybrid cloud deployments.
- Multi-AZ architectures improve reliability and availability.

---

# Summary

In this chapter, you learned:

- AWS Global Infrastructure
- Regions
- Availability Zones
- Data Centers
- Edge Locations
- Regional Edge Caches
- Local Zones
- Wavelength Zones
- AWS Outposts
- High Availability
- Fault Tolerance
- Disaster Recovery
- Choosing the right AWS Region

---

# Interview Questions

## Beginner

1. What is an AWS Region?
2. What is an Availability Zone?
3. What is the difference between a Region and an AZ?
4. What is an Edge Location?
5. Why are multiple AZs important?

---

## Intermediate

6. Explain the purpose of Local Zones.
7. What are Wavelength Zones?
8. How does CloudFront use Edge Locations?
9. What is AWS Outposts?
10. How do you choose an AWS Region?

---

## Advanced

11. Design a highly available web application using AWS infrastructure.
12. Explain Multi-AZ deployment.
13. Compare High Availability and Disaster Recovery.
14. Why are Regions isolated from one another?

---

# Practice Exercises

## Exercise 1

Research three AWS Regions and note:

- Region Code
- Location
- Number of Availability Zones

---

## Exercise 2

Draw the AWS infrastructure hierarchy:

```text
Global Infrastructure
        │
     Region
        │
Availability Zones
        │
   Data Centers
```

---

## Exercise 3

Compare:

- Region
- Availability Zone
- Edge Location

using your own words.

---

## Exercise 4

Choose the best AWS Region for:

- A website serving users in India
- A website serving users in Europe
- A global content delivery application

Explain your reasoning.

---

## Exercise 5

Design a simple architecture with:

- 1 Load Balancer
- 2 EC2 Instances
- 2 Availability Zones

Draw it on paper or using a diagramming tool.

---

# Mini Project

Create a Markdown file named:

```text
aws-global-infrastructure.md
```

Include:

- AWS Global Infrastructure diagram
- Difference between Regions and Availability Zones
- Comparison of Edge Locations, Local Zones, and Wavelength Zones
- High Availability architecture diagram
- Best practices for selecting an AWS Region

Commit the file to your Git repository:

```bash
git add .
git commit -m "Add AWS Global Infrastructure notes"
```

---

# Further Reading

- AWS Regions and Availability Zones
- Amazon CloudFront
- AWS Global Infrastructure
- AWS Well-Architected Framework
- Disaster Recovery on AWS

---

# What's Next?

In **Chapter 03 – IAM (Identity and Access Management)**, you'll learn:

- What IAM is
- IAM Users
- IAM Groups
- IAM Roles
- IAM Policies
- MFA (Multi-Factor Authentication)
- Best security practices
- IAM CLI commands
- Real-world IAM use cases
- Hands-on access management
