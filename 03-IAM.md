# AWS Notes
# Chapter 03 - IAM (Identity and Access Management)

> **Level:** Beginner to Intermediate
> **Estimated Reading Time:** 60–90 minutes
> **Practice Time:** 2–3 hours

---

# Table of Contents

1. Introduction to IAM
2. Why IAM is Important
3. Authentication vs Authorization
4. AWS Account Root User
5. IAM Users
6. IAM Groups
7. IAM Roles
8. IAM Policies
9. IAM Policy Structure (JSON)
10. Types of IAM Policies
11. IAM Permission Evaluation
12. Multi-Factor Authentication (MFA)
13. Password Policies
14. Access Keys
15. AWS CLI Configuration
16. Temporary Credentials
17. Cross-Account Access
18. IAM Best Practices
19. Common IAM Scenarios
20. Hands-on Lab
21. Summary
22. Interview Questions
23. Practice Exercises
24. Mini Project
25. Further Reading

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand AWS Identity and Access Management (IAM)
- Differentiate Authentication and Authorization
- Create IAM Users, Groups, and Roles
- Write and understand IAM Policies
- Secure AWS accounts using MFA
- Configure AWS CLI authentication
- Implement IAM security best practices

---

# What is IAM?

AWS Identity and Access Management (IAM) is a global AWS service that allows you to securely manage access to AWS resources.

IAM helps answer two important questions:

- **Who** can access AWS?
- **What** are they allowed to do?

IAM enables you to:

- Create Users
- Create Groups
- Create Roles
- Assign Permissions
- Enable Multi-Factor Authentication (MFA)
- Secure AWS Resources

> **Note:** IAM is a **Global Service**, not tied to any specific AWS Region.

---

# Why IAM is Important?

Without IAM:

- Anyone with account access could manage all AWS resources.
- Sensitive information could be exposed.
- Resources could be accidentally deleted.
- Security risks would increase significantly.

IAM provides:

- Secure access control
- Fine-grained permissions
- Centralized identity management
- Compliance support
- Auditing and monitoring

---

# Authentication vs Authorization

Authentication verifies **who you are**, while Authorization determines **what you are allowed to do**.

```
User
 │
 ▼
Authentication
(Is the user genuine?)
 │
 ▼
Authorization
(What permissions does the user have?)
 │
 ▼
Access Granted / Denied
```

| Authentication | Authorization |
|---------------|---------------|
| Verifies identity | Determines permissions |
| Username & Password | IAM Policies |
| MFA | Resource Access |

---

# AWS Account Root User

When you create an AWS account, AWS automatically creates a **Root User**.

The Root User has:

- Full administrative access
- Unlimited permissions
- Access to billing and account settings

Use the Root User only for:

- Changing payment methods
- Closing the AWS account
- Changing support plans

## Best Practices

✔ Enable MFA

✔ Never create access keys

✔ Avoid daily usage

---

# IAM Users

An IAM User represents a person or an application requiring AWS access.

Example:

```
Company

├── Alice
├── Bob
├── Charlie
└── DevOps
```

Each user can have:

- Console Password
- Access Keys
- Permissions
- MFA Device

---

# IAM Groups

Groups allow you to manage permissions for multiple users.

Example:

```
Developers

├── Alice
├── Bob
└── Charlie
```

Assign permissions to the group instead of each individual user.

Benefits:

- Easier management
- Consistent permissions
- Better scalability

---

# IAM Roles

Roles provide **temporary credentials** instead of permanent credentials.

Roles are assumed by:

- EC2
- Lambda
- ECS
- EKS
- AWS Services
- External AWS Accounts

Example:

```
EC2 Instance
      │
      ▼
 Assume IAM Role
      │
      ▼
Access Amazon S3
```

Roles improve security by eliminating long-term access keys.

---

# IAM Policies

IAM Policies define permissions.

Policies specify:

- What actions are allowed
- What resources can be accessed
- Whether access is Allowed or Denied

Policies are written in JSON.

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "*"
    }
  ]
}
```

---

# IAM Policy Structure

| Field | Description |
|-------|-------------|
| Version | Policy language version |
| Statement | Permission rules |
| Effect | Allow or Deny |
| Action | AWS API operations |
| Resource | AWS Resource ARN |
| Condition | Optional restrictions |

---

# Types of IAM Policies

## AWS Managed Policies

Created and maintained by AWS.

Examples:

- AmazonS3ReadOnlyAccess
- AmazonEC2FullAccess
- AdministratorAccess

---

## Customer Managed Policies

Created by your organization.

Reusable across multiple users, groups, and roles.

---

## Inline Policies

Attached directly to a single user, group, or role.

Not reusable.

---

# IAM Permission Evaluation

AWS evaluates permissions using the following logic:

```
Request
   │
   ▼
Explicit Deny?
   │
 ┌─┴────────┐
 │ Yes      │
 ▼          ▼
Denied   Allow Exists?
              │
          ┌───┴────┐
          │ Yes    │
          ▼        ▼
      Allowed   Denied
```

> **Important:** Explicit Deny always overrides Allow.

---

# Multi-Factor Authentication (MFA)

MFA adds a second layer of security.

Authentication requires:

- Password
- Verification Code

Supported devices:

- Authenticator Apps
- Hardware Security Keys

Benefits:

- Protects against stolen passwords
- Improves account security

---

# Password Policies

IAM allows administrators to enforce password rules.

Examples:

- Minimum password length
- Uppercase letters
- Lowercase letters
- Numbers
- Special characters
- Password expiration

---

# Access Keys

Access Keys allow programmatic access.

They are used by:

- AWS CLI
- Terraform
- Boto3 (Python)
- Jenkins
- GitHub Actions

Each Access Key consists of:

- Access Key ID
- Secret Access Key

## Best Practices

✔ Rotate keys regularly

✔ Never hardcode credentials

✔ Store securely

---

# Configure AWS CLI

Install AWS CLI.

Configure credentials:

```bash
aws configure
```

Enter:

```
AWS Access Key ID
AWS Secret Access Key
Default Region
Output Format
```

Verify:

```bash
aws sts get-caller-identity
```

---

# Temporary Credentials

Temporary credentials are generated by:

- IAM Roles
- AWS STS
- IAM Identity Center

Advantages:

- Automatic expiration
- Better security
- Reduced credential management

---

# Cross-Account Access

IAM Roles allow one AWS account to access resources in another AWS account.

Example:

```
AWS Account A
       │
 Assume Role
       ▼
AWS Account B
```

Useful for:

- Multi-account environments
- Shared services
- Centralized administration

---

# IAM Best Practices

✔ Never use the Root User for daily tasks

✔ Enable MFA for all users

✔ Use Groups for permission management

✔ Use Roles instead of Access Keys

✔ Apply the Principle of Least Privilege

✔ Rotate credentials regularly

✔ Monitor activity using CloudTrail

✔ Remove unused users and keys

---

# Common IAM Scenarios

| Scenario | Recommended Solution |
|----------|----------------------|
| Developer needs S3 access | IAM Group + Policy |
| EC2 needs S3 access | IAM Role |
| Lambda accesses DynamoDB | IAM Role |
| Temporary employee | IAM User with limited permissions |
| Multi-account management | Cross-Account IAM Role |

---

# Hands-on Lab

## Lab 1

Create:

- One IAM User
- One IAM Group

Assign:

- AmazonS3ReadOnlyAccess

---

## Lab 2

Enable MFA for the IAM User.

---

## Lab 3

Create an IAM Role for EC2 with read-only access to S3.

---

## Lab 4

Configure AWS CLI.

```bash
aws configure
```

Verify:

```bash
aws sts get-caller-identity
```

---

# Key Takeaways

- IAM controls AWS authentication and authorization.
- Root User should only be used for account management.
- Groups simplify permission management.
- Roles provide secure temporary credentials.
- Policies define access permissions.
- Enable MFA for better security.
- Follow the Principle of Least Privilege.

---

# Summary

In this chapter, you learned:

- IAM Fundamentals
- Authentication vs Authorization
- Root User
- IAM Users
- IAM Groups
- IAM Roles
- IAM Policies
- Policy Types
- MFA
- Password Policies
- Access Keys
- AWS CLI
- Temporary Credentials
- Cross-Account Access
- IAM Best Practices

---

# Interview Questions

## Beginner

1. What is IAM?
2. Why is IAM a Global Service?
3. What is the Root User?
4. What is an IAM User?
5. What is an IAM Group?

---

## Intermediate

6. Explain IAM Roles.
7. What is the difference between Users and Roles?
8. What are IAM Policies?
9. What is MFA?
10. Explain Authentication vs Authorization.

---

## Advanced

11. Explain IAM policy evaluation.
12. What is the Principle of Least Privilege?
13. How does Cross-Account Access work?
14. Why are IAM Roles preferred over Access Keys?
15. How would you secure an AWS account?

---

# Practice Exercises

## Exercise 1

Create:

- Two IAM Users
- One IAM Group

Assign permissions using AWS Managed Policies.

---

## Exercise 2

Write an IAM Policy that provides read-only access to an S3 bucket.

---

## Exercise 3

Enable MFA for all IAM users.

---

## Exercise 4

Configure AWS CLI and verify your identity.

```bash
aws sts get-caller-identity
```

---

## Exercise 5

Create an IAM Role for EC2 with S3 ReadOnly permissions.

---

# Mini Project

Create a Markdown file named:

```
iam-security-guide.md
```

Include:

- IAM Architecture Diagram
- Authentication vs Authorization
- Users vs Groups vs Roles
- Sample IAM Policy
- IAM Best Practices
- AWS CLI Configuration Steps

Commit it to Git:

```bash
git add .
git commit -m "Add IAM security guide"
```

---

# Further Reading

- IAM User Guide
- IAM Policy Reference
- AWS STS Documentation
- IAM Best Practices
- AWS Security Best Practices

---

# What's Next?

In **Chapter 04 – Amazon EC2**, you'll learn:

- What is EC2?
- Instance Types
- Amazon Machine Images (AMIs)
- Key Pairs
- Security Groups
- Elastic IP
- User Data
- Launch Templates
- Instance Lifecycle
- Hands-on EC2 Deployment
```
