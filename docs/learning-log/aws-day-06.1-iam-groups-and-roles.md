# AWS Day 06.1 – IAM Groups and IAM Roles

**Date:** 5 March 2026
**Topics:** IAM Groups, IAM Roles, Trust Policies, Permissions Policies

---

# Identity and Access Management (IAM)

**AWS IAM (Identity and Access Management)** is the service used to control access to AWS resources.

It allows administrators to:

* Create identities (users and roles)
* Assign permissions through policies
* Control authentication and authorization

IAM is a **global service** and is foundational to AWS security architecture.

---

# IAM Groups

## What is an IAM Group?

An **IAM Group** is a container for IAM users.

Groups simplify permission management by allowing policies to be assigned to multiple users at once.

Key characteristics:

* Groups contain **IAM users**
* Groups **cannot be logged into**
* Groups **do not have credentials**
* Groups exist only for permission management

Instead of assigning permissions individually to users, administrators attach policies to groups and then add users to those groups.

---

# IAM Policy Evaluation

Permissions for a user are determined by combining:

1. Policies attached directly to the IAM user
2. Policies attached to IAM groups the user belongs to

AWS evaluates permissions using the following order:

1. **Explicit Deny**
2. **Allow**
3. **Implicit (Default) Deny**

Important rule:

> **Explicit Deny always overrides Allow**

If no policy explicitly allows an action, access is denied.

---

# IAM Groups Example

```text id="gx2kj1"
IAM User
│
├── Group: Developers
│   └── Policy: Allow EC2 (Elastic Compute Cloud)
│
└── Group: S3Team
    └── Policy: Allow S3 (Simple Storage Service)
```

Effective permissions for the user:

```text id="ijg2cc"
Allow EC2
Allow S3
```

Permissions from all groups are merged during policy evaluation.

---

# IAM Roles

## What is an IAM Role?

An **IAM Role** is an AWS identity that provides **temporary access permissions**.

Unlike IAM users:

* Roles have **no permanent credentials**
* Roles are **assumed temporarily**
* Roles are used by **trusted identities**

Roles are commonly used when:

* AWS services need permissions
* Multiple identities require the same permissions
* Temporary access is preferred over long-term credentials

When a role is assumed, AWS generates **temporary security credentials using AWS STS (Security Token Service).**

---

# IAM Role Architecture

```text id="fc6l4o"
Identity
│
└── Assume Role
        ↓
    IAM Role
        │
        ├── Trust Policy
        │     (who can assume the role)
        │
        └── Permissions Policy
              (what the role can do)
```

---

# Trust Policy

The **Trust Policy** defines which identities are allowed to assume the role.

Examples of trusted identities include:

* AWS services (EC2 – Elastic Compute Cloud)
* IAM users
* IAM roles
* External identity providers

Trust policies determine **who is allowed to use the role**.

---

# Permissions Policy

The **Permissions Policy** defines what actions the role can perform once it has been assumed.

Example permissions:

* Access S3 (Simple Storage Service)
* Launch EC2 instances
* Write logs to CloudWatch (Amazon CloudWatch)

Permissions policies determine **what the role is allowed to do**.

---

# Role Assumption Flow

```text id="z1z6t3"
User / Service
      │
      └── Assume Role
              ↓
        AWS STS
        (Security Token Service)
              ↓
      Temporary Security Credentials
              ↓
        Access AWS Resources
```

---

# Architectural Takeaways

* IAM Groups simplify permission management for multiple users
* IAM Roles provide **temporary access** without long-term credentials
* Trust Policies define **who can assume a role**
* Permissions Policies define **what actions the role can perform**
* Temporary credentials generated through **AWS STS improve security**

---

# References

Concepts reinforced through:

* AWS Documentation
* Adrian Cantrill – AWS Solutions Architect Associate Course
