# AWS Notes
# Chapter 26 - AWS CloudFormation

> 📘 **Level:** Beginner to Intermediate
> ⏱️ **Estimated Reading Time:** 60–75 minutes
> 🛠️ **Practice Time:** 3–4 hours

---

# 📚 Table of Contents

1. What is Infrastructure as Code (IaC)?
2. What is AWS CloudFormation?
3. Why Use CloudFormation?
4. CloudFormation Architecture
5. CloudFormation Workflow
6. Template Structure
7. Resources
8. Parameters
9. Mappings
10. Conditions
11. Outputs
12. Metadata
13. Intrinsic Functions
14. Pseudo Parameters
15. Stacks
16. Nested Stacks
17. StackSets
18. Change Sets
19. Drift Detection
20. Stack Policies
21. Rollback
22. CloudFormation Designer
23. YAML vs JSON
24. AWS CLI Commands
25. Best Practices
26. Common Use Cases
27. Summary
28. Interview Questions
29. Practice Exercises
30. Mini Project
31. Further Reading

---

# 🎯 Learning Objectives

After completing this chapter, you will be able to:

- Understand Infrastructure as Code (IaC)
- Create CloudFormation templates
- Deploy AWS infrastructure automatically
- Manage stacks and updates
- Detect infrastructure drift
- Follow CloudFormation best practices

---

# 📖 What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is the practice of defining and managing infrastructure using code instead of manual configuration.

Benefits:

- ✅ Automation
- ✅ Version Control
- ✅ Consistency
- ✅ Repeatability
- ✅ Faster Deployments

---

# ☁️ What is AWS CloudFormation?

AWS CloudFormation is an **Infrastructure as Code (IaC)** service that allows you to create, update, and manage AWS resources using templates.

Supported template formats:

- YAML
- JSON

---

# 💡 Why Use CloudFormation?

Instead of creating resources manually:

```text
Login → Create VPC → Create EC2 → Create RDS
```

Use a template:

```text
Template
     │
     ▼
CloudFormation
     │
     ▼
Infrastructure Created Automatically
```

Benefits:

- Automated deployments
- Easy updates
- Version-controlled infrastructure
- Repeatable environments

---

# 🏗️ CloudFormation Architecture

```text
Developer
     │
     ▼
YAML / JSON Template
     │
     ▼
CloudFormation Stack
     │
     ▼
AWS Resources
 ├── EC2
 ├── VPC
 ├── S3
 ├── IAM
 └── RDS
```

---

# 🔄 CloudFormation Workflow

```text
Create Template

↓

Upload Template

↓

Create Stack

↓

Provision Resources

↓

Update/Delete Stack
```

---

# 📄 Template Structure

A CloudFormation template contains sections like:

- AWSTemplateFormatVersion
- Description
- Parameters
- Mappings
- Conditions
- Resources
- Outputs

Example:

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: Sample Template
Resources:
```

---

# 📦 Resources

The **Resources** section defines AWS services to create.

Examples:

- EC2
- S3
- VPC
- IAM
- RDS

Example:

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
```

---

# ⚙️ Parameters

Parameters allow users to provide input values.

Example:

```yaml
Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
```

Benefits:

- Reusable templates
- Dynamic configuration

---

# 🗺️ Mappings

Mappings store fixed values.

Example:

```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-123456
```

Used for:

- Region-specific AMIs
- Environment settings

---

# 🔀 Conditions

Conditions control resource creation.

Example:

```yaml
Conditions:
  CreateProd: !Equals [!Ref Env, prod]
```

Useful for:

- Production
- Development
- Testing

---

# 📤 Outputs

Outputs return useful information.

Example:

```yaml
Outputs:
  BucketName:
    Value: !Ref MyBucket
```

Examples:

- EC2 Public IP
- Load Balancer DNS
- VPC ID

---

# 🏷️ Metadata

Stores additional template information.

Example:

```yaml
Metadata:
  Author: DevOps Team
```

Used for documentation.

---

# 🔧 Intrinsic Functions

CloudFormation provides built-in functions.

Common functions:

- !Ref
- !Sub
- !GetAtt
- !Join
- !Split
- !Select
- !FindInMap
- !If
- !ImportValue

Example:

```yaml
BucketName: !Ref MyBucket
```

---

# 🌍 Pseudo Parameters

AWS automatically provides values.

Examples:

- AWS::Region
- AWS::AccountId
- AWS::StackName
- AWS::Partition

Example:

```yaml
!Ref AWS::Region
```

---

# 📚 Stacks

A Stack is a collection of AWS resources managed together.

Example:

```text
Stack

├── VPC
├── EC2
├── S3
└── IAM
```

---

# 🪆 Nested Stacks

Large templates can be divided into smaller stacks.

Benefits:

- Reusability
- Easy maintenance
- Modular design

---

# 🌎 StackSets

Deploy the same stack across:

- Multiple AWS Accounts
- Multiple AWS Regions

Useful for enterprise environments.

---

# 🔄 Change Sets

Preview infrastructure changes before applying them.

Benefits:

- Safer deployments
- Avoid accidental changes

---

# 🔍 Drift Detection

Checks whether resources were modified outside CloudFormation.

Example:

```text
CloudFormation

↓

Compare

↓

Detect Drift
```

---

# 🛡️ Stack Policies

Protect critical resources from updates.

Example:

- Prevent database deletion
- Prevent VPC modification

---

# ↩️ Rollback

If deployment fails:

```text
Create Stack

↓

Failure

↓

Rollback

↓

Previous State Restored
```

---

# 🎨 CloudFormation Designer

Visual tool for:

- Designing templates
- Editing resources
- Viewing architecture

---

# 📄 YAML vs JSON

| YAML | JSON |
|-------|------|
| Easy to read | Verbose |
| Less syntax | More brackets |
| Preferred | Supported |

YAML is recommended.

---

# 💻 Useful AWS CLI Commands

Create Stack

```bash
aws cloudformation create-stack
```

List Stacks

```bash
aws cloudformation list-stacks
```

Describe Stack

```bash
aws cloudformation describe-stacks
```

Delete Stack

```bash
aws cloudformation delete-stack
```

Validate Template

```bash
aws cloudformation validate-template
```

---

# 🏆 Best Practices

- ✅ Use YAML templates
- ✅ Split large templates
- ✅ Use Parameters
- ✅ Enable Change Sets
- ✅ Use Stack Policies
- ✅ Store templates in Git
- ✅ Reuse Nested Stacks
- ✅ Follow least privilege IAM

---

# 🌍 Common Use Cases

- Deploy VPC
- Launch EC2
- Create S3 Buckets
- Deploy RDS
- Create IAM Roles
- Deploy Load Balancers
- Complete Infrastructure Automation

---

# 📝 Key Takeaways

- CloudFormation is AWS Infrastructure as Code service.
- Templates are written in YAML or JSON.
- Resources are deployed as Stacks.
- Supports automation and repeatability.
- Integrates with most AWS services.
- Ideal for DevOps and CI/CD pipelines.

---

# 📋 Summary

In this chapter, you learned:

- Infrastructure as Code
- CloudFormation
- Templates
- Resources
- Parameters
- Mappings
- Conditions
- Outputs
- Intrinsic Functions
- Stacks
- Nested Stacks
- StackSets
- Drift Detection
- Rollback
- AWS CLI
- Best Practices

---

# ❓ Interview Questions

## Beginner

1. What is AWS CloudFormation?
2. What is Infrastructure as Code?
3. What is a Stack?
4. Why use CloudFormation?
5. What template formats are supported?

---

## Intermediate

6. Explain Parameters.
7. What are Outputs?
8. What are Nested Stacks?
9. What is Drift Detection?
10. Explain Change Sets.

---

## Advanced

11. CloudFormation vs Terraform?
12. Explain StackSets.
13. How does Rollback work?
14. How do you secure CloudFormation deployments?
15. How would you deploy a multi-tier application using CloudFormation?

---

# 🎯 Practice Exercises

1. Create your first CloudFormation template.
2. Deploy an S3 bucket.
3. Create an EC2 instance using YAML.
4. Update an existing stack.
5. Delete the stack after testing.

---

# 🧩 Mini Project

Create a file named:

```text
cloudformation-project.yaml
```

Deploy:

- VPC
- Public Subnet
- EC2 Instance
- Security Group
- S3 Bucket

Manage the entire infrastructure using CloudFormation.

---

# 📚 Further Reading

- AWS CloudFormation Documentation
- AWS Well-Architected Framework
- AWS CLI Reference
- CloudFormation Template Reference
- AWS DevOps Best Practices

---

# 🚀 What's Next?

In **Chapter 27 – AWS CodeCommit**, you'll learn:

- 🗂️ Git Repository on AWS
- 🌿 Branches and Commits
- 🔀 Pull Requests
- 👥 Repository Permissions
- 🔐 IAM Integration
- 💻 AWS CLI Commands
- 🚀 CI/CD Integration
- 🛠️ Hands-on Git Projects
