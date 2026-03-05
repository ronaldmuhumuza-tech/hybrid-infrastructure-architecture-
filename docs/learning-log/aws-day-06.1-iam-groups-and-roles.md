# AWS Day 06 – IAM Groups and IAM Roles
**Date:** 5 March 2026  
**Topics:** IAM Groups, IAM Roles, Trust Policies, Permissions Policies

---

# IAM Groups

## What is an IAM Group?

An **Identity and Access Management (IAM)** group is a container for IAM users.

Groups simplify permission management by allowing policies to be applied to multiple users at once.

Key characteristics:

- Groups contain **IAM users**
- Groups **cannot be logged into**
- Groups **do not have credentials**
- Groups exist only for permission management

---

# IAM Policy Evaluation

Permissions for a user are determined by merging:

1. Policies attached directly to the IAM user
2. Policies attached to IAM groups the user belongs to

AWS evaluates permissions using the following logic:

1. Explicit Deny
2. Allow
3. Default Deny

Important rule:

**Explicit Deny always overrides Allow**

---

# IAM Groups Example

IAM User
│
├── Group: Developers
│ └── Policy: Allow EC2
│
└── Group: S3Team
└── Policy: Allow S3


Effective permissions:
Allow EC2
Allow S3


---

# IAM Roles

## What is an IAM Role?

An IAM role is an identity that provides **temporary access permissions**.

Unlike IAM users:

- Roles have **no permanent credentials**
- Roles are **assumed temporarily**

Roles are used when:

- Many identities require the same permissions
- Access must be temporary
- Long-term credentials should not be stored

---

# IAM Role Architecture

Identity
│
└── Assume Role
↓
IAM Role
│
├── Trust Policy (who can assume role)
└── Permissions Policy (what the role can do)

---

# Trust Policy

The **trust policy** defines which identities can assume the role.

Examples:

- AWS services (EC2 – Elastic Compute Cloud)
- IAM users
- IAM roles
- External identity providers

---

# Permissions Policy

Defines what the role can do after it is assumed.

Example permissions:

- Access S3 (Simple Storage Service)
- Launch EC2 instances
- Write logs to CloudWatch

---

# Architectural Takeaways

- Groups simplify permission management
- Roles enable temporary secure access
- Trust policies control *who can assume*
- Permissions policies control *what can be done*

---

## References

Concepts in this study note were reinforced through:

- AWS Documentation
- Adrian Cantrill – AWS Solutions Architect Associate Course
