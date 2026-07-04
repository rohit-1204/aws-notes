# AWS Notes
# Chapter 20 - Amazon CloudWatch

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 75–90 minutes
> 🛠️ **Practice Time:** 4–5 hours

---

# 📚 Table of Contents

1. What is Amazon CloudWatch?
2. Why Use CloudWatch?
3. CloudWatch Components
4. Metrics
5. Namespaces
6. Dimensions
7. CloudWatch Logs
8. Log Groups & Log Streams
9. CloudWatch Alarms
10. CloudWatch Events (EventBridge)
11. Dashboards
12. CloudWatch Agent
13. CloudWatch Insights
14. CloudWatch Architecture
15. AWS CLI Commands
16. Best Practices
17. Common Use Cases
18. Summary
19. Interview Questions
20. Practice Exercises
21. Mini Project
22. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Amazon CloudWatch
- Monitor AWS resources
- Create CloudWatch Alarms
- Collect and analyze logs
- Build monitoring dashboards
- Automate actions using EventBridge

---

# 📖 What is Amazon CloudWatch?

**Amazon CloudWatch** is AWS's monitoring and observability service.

It collects and monitors:

- 📊 Metrics
- 📄 Logs
- 🚨 Alarms
- 📈 Dashboards
- ⚡ Events

CloudWatch helps you monitor application health, infrastructure, and AWS services in real time.

---

# 💡 Why Use CloudWatch?

Without monitoring:

```text
Application

↓

Server Stops

↓

Nobody Knows
```

Problems:

- ❌ Downtime
- ❌ Slow troubleshooting
- ❌ No alerts

---

With CloudWatch:

```text
Application

↓

CloudWatch

↓

Alarm

↓

SNS Notification

↓

Administrator
```

Benefits:

- ✅ Real-time monitoring
- ✅ Alerts
- ✅ Performance analysis
- ✅ Automated actions

---

# 🧠 CloudWatch Components

CloudWatch includes:

- 📊 Metrics
- 📄 Logs
- 🚨 Alarms
- 📈 Dashboards
- ⚡ Events (Amazon EventBridge)
- 🔍 Logs Insights
- 🖥️ CloudWatch Agent

---

# 📊 Metrics

Metrics are numerical data collected over time.

Examples:

| AWS Service | Metrics |
|-------------|----------|
| EC2 | CPU Utilization |
| EBS | Read/Write Operations |
| ALB | Request Count |
| RDS | Database Connections |
| Lambda | Invocations |
| DynamoDB | Read Capacity |

Example:

```text
CPU Utilization

80%

↓

CloudWatch Metric
```

---

# 📂 Namespaces

Metrics are grouped into namespaces.

Examples:

| Namespace | Service |
|------------|----------|
| AWS/EC2 | EC2 |
| AWS/RDS | RDS |
| AWS/S3 | S3 |
| AWS/Lambda | Lambda |
| AWS/ApplicationELB | ALB |

---

# 🏷️ Dimensions

Dimensions provide additional information about metrics.

Example:

```text
Metric:

CPU Utilization

Dimension:

Instance ID

↓

i-0123456789abcdef
```

Dimensions help identify the exact AWS resource.

---

# 📄 CloudWatch Logs

CloudWatch Logs stores application and system logs.

Examples:

- EC2 Logs
- Lambda Logs
- Application Logs
- Web Server Logs
- VPC Flow Logs

Example:

```text
Application

↓

Log File

↓

CloudWatch Logs
```

---

# 📁 Log Groups & Log Streams

CloudWatch organizes logs into:

### Log Group

A collection of related log streams.

Example:

```
/aws/ec2/webserver
```

---

### Log Stream

A sequence of log events from one source.

Example:

```
EC2-Server-01
```

Structure:

```text
Log Group

│

├── Log Stream 1

├── Log Stream 2

└── Log Stream 3
```

---

# 🚨 CloudWatch Alarms

CloudWatch Alarms monitor metrics and trigger actions.

Example:

```text
CPU > 80%

↓

Alarm

↓

Send Email

↓

Scale EC2
```

Possible actions:

- SNS Notification
- Auto Scaling
- Lambda Function
- EC2 Recovery

---

# 🔔 Alarm States

CloudWatch Alarms have three states.

| State | Meaning |
|---------|----------|
| OK | Everything is normal |
| ALARM | Threshold exceeded |
| INSUFFICIENT_DATA | Not enough data |

---

# ⚡ Amazon EventBridge (CloudWatch Events)

EventBridge responds to AWS events automatically.

Example:

```text
EC2 Stopped

↓

EventBridge Rule

↓

Lambda Function

↓

Send Email
```

Common triggers:

- EC2 State Change
- S3 Upload
- IAM Changes
- CodePipeline Events

---

# 📈 CloudWatch Dashboards

Dashboards display multiple metrics in one place.

Example:

```text
Dashboard

CPU Usage

Memory Usage

Disk Usage

Network Traffic

Requests/sec
```

Useful for monitoring production environments.

---

# 🖥️ CloudWatch Agent

The CloudWatch Agent collects additional metrics from EC2 instances.

Examples:

- Memory Usage
- Disk Usage
- Swap Usage
- Running Processes

Without the agent, EC2 sends only basic metrics.

---

# 🔍 CloudWatch Logs Insights

CloudWatch Logs Insights allows you to search and analyze logs.

Example Query:

```sql
fields @timestamp, @message
| sort @timestamp desc
| limit 20
```

Useful for:

- Error analysis
- Debugging
- Log filtering

---

# 🏗️ CloudWatch Architecture

```text
          AWS Resources
     ┌────────┬─────────┐
     ▼        ▼         ▼
    EC2      RDS      Lambda
       \      │        /
        \     │       /
         ▼    ▼      ▼
        Amazon CloudWatch
        ├──────────────┐
        ▼              ▼
     Metrics         Logs
        │              │
        ▼              ▼
     Alarms       Dashboards
        │
        ▼
 SNS / Auto Scaling / Lambda
```

---

# 💻 Useful AWS CLI Commands

## List Metrics

```bash
aws cloudwatch list-metrics
```

---

## Get Metric Statistics

```bash
aws cloudwatch get-metric-statistics \
--namespace AWS/EC2 \
--metric-name CPUUtilization
```

---

## Create Alarm

```bash
aws cloudwatch put-metric-alarm \
--alarm-name HighCPU
```

---

## List Alarms

```bash
aws cloudwatch describe-alarms
```

---

## List Log Groups

```bash
aws logs describe-log-groups
```

---

## List Log Streams

```bash
aws logs describe-log-streams \
--log-group-name /aws/ec2/webserver
```

---

# 💡 Best Practices

✅ Monitor critical resources.

✅ Create alarms for CPU, memory, and disk.

✅ Use CloudWatch Agent for detailed metrics.

✅ Centralize logs in CloudWatch Logs.

✅ Build dashboards for production environments.

✅ Enable log retention policies.

✅ Integrate with SNS for notifications.

✅ Use EventBridge for automation.

---

# 🌍 Common Use Cases

| Scenario | CloudWatch Feature |
|-----------|--------------------|
| Server Monitoring | Metrics |
| Log Analysis | CloudWatch Logs |
| Notifications | Alarms + SNS |
| Auto Scaling | Alarms |
| Dashboards | Monitoring |
| Automation | EventBridge |
| Troubleshooting | Logs Insights |

---

# 📝 Key Takeaways

- CloudWatch monitors AWS resources.
- Metrics measure performance.
- Logs store application events.
- Alarms notify administrators.
- Dashboards provide centralized monitoring.
- EventBridge automates responses.
- CloudWatch Agent collects additional system metrics.

---

# 📋 Summary

In this chapter, you learned:

- Amazon CloudWatch
- Metrics
- Namespaces
- Dimensions
- CloudWatch Logs
- Log Groups
- Log Streams
- Alarms
- EventBridge
- Dashboards
- CloudWatch Agent
- Logs Insights
- AWS CLI Commands
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is Amazon CloudWatch?
2. What are metrics?
3. What is CloudWatch Logs?
4. What is a CloudWatch Alarm?
5. What is a Dashboard?

---

## Intermediate

6. Explain Log Groups and Log Streams.
7. What are Dimensions?
8. How does EventBridge work?
9. Why do we need CloudWatch Agent?
10. What is Logs Insights?

---

## Advanced

11. Design a monitoring solution for a production application.
12. How would you monitor EC2 memory utilization?
13. Explain CloudWatch integration with Auto Scaling.
14. How do CloudWatch Alarms trigger automated actions?
15. Compare CloudWatch Metrics and CloudWatch Logs.

---

# 🎯 Practice Exercises

## Exercise 1

Create a CloudWatch Dashboard.

---

## Exercise 2

Monitor EC2 CPU Utilization.

---

## Exercise 3

Create an Alarm when CPU exceeds **80%**.

---

## Exercise 4

Install CloudWatch Agent and monitor memory usage.

---

## Exercise 5

Create a Log Group and view application logs.

---

# 🧩 Mini Project

Create a Markdown file named:

```text
aws-cloudwatch-guide.md
```

Include:

- CloudWatch Overview
- Metrics
- Namespaces
- Dimensions
- CloudWatch Logs
- Alarms
- Dashboards
- EventBridge
- CloudWatch Agent
- Logs Insights
- AWS CLI Commands
- Best Practices

Commit it to Git:

```bash
git add .
git commit -m "Add Amazon CloudWatch guide"
```

---

# 📚 Further Reading

- Amazon CloudWatch Documentation
- CloudWatch Logs User Guide
- Amazon EventBridge Documentation
- AWS Monitoring Best Practices
- AWS Well-Architected Framework

---

# 🚀 What's Next?

In **Chapter 21 – AWS IAM (Identity and Access Management)**, you'll learn:

- 👤 IAM Users
- 👥 IAM Groups
- 🎭 IAM Roles
- 📜 IAM Policies
- 🔑 Access Keys
- 🔐 Multi-Factor Authentication (MFA)
- 🌐 Cross-Account Access
- 🛡️ IAM Security Best Practices
- 💻 AWS CLI Commands
- 🚀 Hands-on IAM Labs
