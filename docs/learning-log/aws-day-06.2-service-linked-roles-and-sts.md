# AWS Day 06 – Service-Linked Roles and STS
**Date:** 5 March 2026  
**Topics:** Service-Linked Roles, PassRole Permission, STS (Security Token Service)

---

# Service-Linked Roles

## What is a Service-Linked Role?

A **Service-Linked Role (SLR – Service Linked Role)** is a special IAM role tied to a specific AWS service.

It allows the service to perform actions in your account.

Example services using service-linked roles:

- Auto Scaling
- Elastic Load Balancing
- Amazon RDS (Relational Database Service)
- AWS Lambda

---

# Service-Linked Role Architecture
AWS Service
    │
    └── Assumes
            ↓
      Service-Linked Role
            │
            └── Permissions to interact with other AWS services


Example:

Auto Scaling may need permissions to:

- Launch EC2 instances
- Attach Load Balancers
- Modify scaling groups

---

# Key Characteristics

- Linked to a specific service
- Automatically created by AWS
- Cannot be deleted while service is using it
- Trust policy only allows the service to assume it

---

# iam:PassRole Permission

The IAM permission:
iam:PassRole


Allows a user to pass an IAM role to an AWS service.

Example:

A developer launches an EC2 instance and assigns a role.

Without `iam:PassRole`, the user cannot attach the role.

---

# Why PassRole Matters

PassRole prevents privilege escalation.

Without restriction:

A developer could attach an **Administrator role** to an EC2 instance they control.

That instance would gain full administrative access.

Therefore PassRole should always be tightly controlled.

---

# AWS STS – Security Token Service

**STS (Security Token Service)** generates temporary security credentials.

Credentials include:

- Access Key ID
- Secret Access Key
- Session Token

These credentials expire after a short period.

---

# Role Assumption Flow
Identity (User / Application / Service)
        │
        └── Assume Role
                ↓
        AWS STS (Security Token Service)
                ↓
        Temporary Security Credentials
                ↓
        Access AWS Resources

# Real-World Example
When creating an Auto Scaling group, AWS may automatically create the role:
AWSServiceRoleForAutoScaling

This service-linked role allows Auto Scaling to:
- launch EC2 instances
- attach load balancers
- modify scaling groups
- 
---

# Architectural Takeaways

- Prefer temporary credentials over long-term access keys
- Use service-linked roles for AWS service permissions
- Restrict iam:PassRole permissions carefully
- STS improves security by limiting credential lifetime


