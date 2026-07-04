# AWS Notes
# Chapter 15 - Auto Scaling Groups (ASG)

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Auto Scaling?
2. Why Do We Need Auto Scaling?
3. How Auto Scaling Works
4. Auto Scaling Components
5. Launch Templates
6. Auto Scaling Groups (ASG)
7. Desired, Minimum & Maximum Capacity
8. Scaling Policies
9. Dynamic Scaling
10. Predictive Scaling
11. Scheduled Scaling
12. Health Checks
13. ELB Integration
14. Auto Scaling Lifecycle
15. Scaling Process
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

- Understand Auto Scaling
- Configure Auto Scaling Groups
- Create Launch Templates
- Configure Scaling Policies
- Integrate ELB with ASG
- Build highly available and cost-efficient applications

---

# 📖 What is Auto Scaling?

**AWS Auto Scaling** automatically adds or removes EC2 instances based on your application's workload.

It ensures that:

- 📈 Applications handle increased traffic
- 💰 Costs are optimized
- 🛡️ High availability is maintained
- ⚡ Resources scale automatically

---

# 💡 Why Do We Need Auto Scaling?

Imagine your website receives:

- 500 users in the morning
- 5,000 users during lunch
- 50,000 users during a sale

Without Auto Scaling:

```text
Users
   │
   ▼
2 EC2 Instances
```

Problems:

- ❌ Server overload
- ❌ Slow response
- ❌ Downtime

---

With Auto Scaling:

```text
Morning

Users
   │
   ▼
2 EC2 Instances

------------------------

Peak Hours

Users
   │
   ▼
8 EC2 Instances

------------------------

Night

Users
   │
   ▼
2 EC2 Instances
```

AWS automatically adjusts the number of instances.

---

# 🧠 How Auto Scaling Works

```text
CloudWatch Metrics
        │
        ▼
Scaling Policy
        │
        ▼
Auto Scaling Group
        │
 ┌──────┴─────────┐
 ▼                ▼
Launch EC2    Terminate EC2
```

CloudWatch monitors metrics like CPU utilization and triggers scaling actions.

---

# 🏗️ Auto Scaling Components

Auto Scaling consists of:

- 🚀 Launch Template
- 👥 Auto Scaling Group (ASG)
- 📊 Scaling Policies
- ❤️ Health Checks
- 📈 CloudWatch Alarms
- ⚖️ Elastic Load Balancer (Optional)

---

# 🚀 Launch Template

A **Launch Template** defines how new EC2 instances should be launched.

It includes:

- AMI
- Instance Type
- Key Pair
- Security Group
- IAM Role
- User Data
- Storage (EBS)

Example:

```text
Launch Template

AMI:
Amazon Linux 2023

Instance:
t3.micro

Security Group:
WebServerSG

Volume:
20 GB
```

---

# 👥 Auto Scaling Group (ASG)

An **Auto Scaling Group** manages a collection of EC2 instances.

Responsibilities:

- Launch new instances
- Replace unhealthy instances
- Remove unnecessary instances
- Maintain desired capacity

---

# 📊 Desired, Minimum & Maximum Capacity

Example:

```text
Minimum = 2

Desired = 3

Maximum = 8
```

Meaning:

- AWS always keeps at least **2** instances.
- Normally runs **3** instances.
- Can scale up to **8** instances.

---

Visualization:

```text
Maximum
████████

Desired
███

Minimum
██
```

---

# 📈 Scaling Policies

Scaling Policies define **when** Auto Scaling should launch or terminate instances.

Common policies:

- Target Tracking Scaling
- Simple Scaling
- Step Scaling

---

# 🎯 Target Tracking Scaling

Automatically keeps a metric close to a target value.

Example:

```text
Target CPU = 60%
```

If CPU exceeds 60%:

➜ Launch new EC2

If CPU drops below target:

➜ Remove EC2

---

# ⚡ Simple Scaling

Uses CloudWatch Alarms.

Example:

```text
CPU > 70%

Launch 1 EC2
```

---

# 📉 Step Scaling

Scales differently depending on the metric value.

Example:

| CPU Usage | Action |
|-----------|--------|
| >60% | Add 1 EC2 |
| >75% | Add 2 EC2 |
| >90% | Add 4 EC2 |

More flexible than Simple Scaling.

---

# 🔮 Predictive Scaling

AWS uses machine learning to predict future demand.

Example:

Every weekday at 9 AM:

Traffic increases.

AWS launches instances **before** traffic arrives.

Benefits:

- Better user experience
- Reduced latency
- Faster scaling

---

# 📅 Scheduled Scaling

Useful for predictable workloads.

Example:

```text
9:00 AM

Scale to 10 Instances

-------------------

8:00 PM

Scale back to 2 Instances
```

Ideal for:

- Office applications
- Business hours
- Batch processing

---

# ❤️ Health Checks

Auto Scaling continuously checks instance health.

Sources:

- EC2 Status Checks
- Elastic Load Balancer Health Checks

If an instance fails:

```text
Unhealthy EC2

↓

Terminate

↓

Launch New EC2
```

Replacement happens automatically.

---

# ⚖️ ELB Integration

ASG works seamlessly with Elastic Load Balancer.

Architecture:

```text
Internet
     │
     ▼
Application Load Balancer
     │
 ┌───┴─────────────┐
 ▼                 ▼
EC2-1           EC2-2
     │
     ▼
Auto Scaling Group
```

New instances are automatically registered with the Load Balancer.

---

# 🔄 Auto Scaling Lifecycle

```text
Create Launch Template
          │
          ▼
Create Auto Scaling Group
          │
          ▼
Launch EC2 Instances
          │
          ▼
Monitor Metrics
          │
          ▼
Scale Out / Scale In
          │
          ▼
Replace Unhealthy Instances
```

---

# 📈 Scaling Process

Example:

```text
CPU = 25%

↓

2 EC2 Instances

------------------------

CPU = 80%

↓

Launch 2 More

↓

4 EC2 Instances

------------------------

CPU = 15%

↓

Terminate 2

↓

2 EC2 Instances
```

---

# 💻 Useful AWS CLI Commands

## Create Launch Template

```bash
aws ec2 create-launch-template \
--launch-template-name WebTemplate
```

---

## Create Auto Scaling Group

```bash
aws autoscaling create-auto-scaling-group \
--auto-scaling-group-name WebASG \
--launch-template LaunchTemplateName=WebTemplate \
--min-size 2 \
--max-size 6 \
--desired-capacity 3 \
--vpc-zone-identifier subnet-xxxx,subnet-yyyy
```

---

## Describe Auto Scaling Groups

```bash
aws autoscaling describe-auto-scaling-groups
```

---

## Update Desired Capacity

```bash
aws autoscaling set-desired-capacity \
--auto-scaling-group-name WebASG \
--desired-capacity 4
```

---

## Delete Auto Scaling Group

```bash
aws autoscaling delete-auto-scaling-group \
--auto-scaling-group-name WebASG \
--force-delete
```

---

# 💡 Best Practices

✅ Use Launch Templates instead of Launch Configurations.

✅ Distribute instances across multiple Availability Zones.

✅ Integrate with an Application Load Balancer.

✅ Enable Health Checks.

✅ Use Target Tracking Scaling for most workloads.

✅ Monitor metrics with CloudWatch.

✅ Configure proper Minimum and Maximum Capacity.

✅ Test scaling events before production deployment.

---

# 🌍 Common Use Cases

| Scenario | Auto Scaling |
|----------|--------------|
| E-commerce Website | ✅ |
| Web Applications | ✅ |
| APIs | ✅ |
| Gaming Servers | ✅ |
| Microservices | ✅ |
| Seasonal Traffic | ✅ |
| Event-Based Applications | ✅ |

---

# 📝 Key Takeaways

- Auto Scaling automatically adjusts EC2 capacity.
- Launch Templates define instance configuration.
- Auto Scaling Groups manage EC2 instances.
- Scaling Policies determine when to scale.
- CloudWatch triggers scaling events.
- ELB distributes traffic to healthy instances.
- Health Checks replace failed instances automatically.

---

# 📋 Summary

In this chapter, you learned:

- Auto Scaling
- Launch Templates
- Auto Scaling Groups
- Desired, Minimum & Maximum Capacity
- Scaling Policies
- Target Tracking
- Step Scaling
- Predictive Scaling
- Scheduled Scaling
- Health Checks
- ELB Integration
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Auto Scaling?
2. Why do we use Auto Scaling?
3. What is a Launch Template?
4. What is an Auto Scaling Group?
5. What is Desired Capacity?

---

## Intermediate

6. Explain Target Tracking Scaling.
7. Differentiate Step Scaling and Simple Scaling.
8. How does Auto Scaling integrate with ELB?
9. What are Health Checks?
10. Explain Scheduled Scaling.

---

## Advanced

11. Design a highly available web application using ASG and ALB.
12. How does Predictive Scaling work?
13. Explain the Auto Scaling lifecycle.
14. How would you troubleshoot instances that continuously terminate?
15. How do you optimize Auto Scaling for cost and performance?

---

# 🎯 Practice Exercises

## Exercise 1

Create a Launch Template using Amazon Linux.

---

## Exercise 2

Create an Auto Scaling Group with:

- Minimum: 2
- Desired: 3
- Maximum: 5

---

## Exercise 3

Attach the Auto Scaling Group to an Application Load Balancer.

---

## Exercise 4

Create a Target Tracking Policy with:

```text
CPU Utilization = 60%
```

---

## Exercise 5

Generate CPU load on your EC2 instances and observe Auto Scaling launching new instances.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-auto-scaling-guide.md
```

Include:

- Auto Scaling Overview
- Launch Templates
- Auto Scaling Groups
- Scaling Policies
- Target Tracking
- Predictive Scaling
- Scheduled Scaling
- Health Checks
- ELB Integration
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Auto Scaling guide"
```

---

# 📚 Further Reading

- AWS Auto Scaling Documentation
- Amazon EC2 Auto Scaling User Guide
- AWS CloudWatch Documentation
- Elastic Load Balancing Documentation
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 16 – Amazon S3 (Simple Storage Service)**, you'll learn:

- 🪣 What is Amazon S3?
- 🏗️ Buckets and Objects
- 📂 Storage Classes
- 🔐 Bucket Policies & ACLs
- 🌍 Static Website Hosting
- 🔄 Versioning
- ♻️ Lifecycle Policies
- 🔒 Encryption
- 📊 S3 Event Notifications
- 💻 AWS CLI Commands
- 🏆 Best Practices
