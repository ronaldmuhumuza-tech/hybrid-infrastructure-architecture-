# AWS Day 06 – AWS Organizations and Service Control Policies

**Date:** 5 March 2026
**Topics:** AWS Organizations, Organizational Units (OU), Service Control Policies (SCP)

---

# AWS Organizations

**AWS Organizations** is a service that enables centralized management and governance of multiple AWS accounts.

It allows organizations to structure environments, enforce security controls, and manage billing across accounts from a single management account.

Key benefits include:

* **Centralized governance** across multiple AWS accounts
* **Consolidated billing** for simplified cost management
* **Policy enforcement** using Service Control Policies (SCP)

AWS Organizations is commonly used in enterprise environments to enforce security guardrails and maintain consistent architecture standards across teams.

---

# Organizational Structure

AWS Organizations uses a hierarchical structure where accounts can be grouped into Organizational Units.

```
Root
│
├── Security OU
│   └── Security Account
│
├── Production OU
│   ├── App1 Account
│   └── App2 Account
│
└── Development OU
    ├── Dev Account
    └── Test Account
```

Accounts are grouped into **Organizational Units (OU)** to simplify policy management and governance.

---

# Management Account

The **Management Account** is the primary account that creates and manages the AWS Organization.

It is also referred to as the **Payer Account**, because it receives the consolidated bill for all member accounts.

Responsibilities include:

* Managing the AWS Organization
* Creating new accounts or inviting existing accounts
* Applying organization-level policies
* Managing consolidated billing

Important:

> The **Management Account cannot be restricted by Service Control Policies (SCP)**.

This ensures administrators cannot accidentally lock themselves out of managing the organization.

---

# Organizational Units (OU)

**OU – Organizational Unit**

Organizational Units are logical containers used to group AWS accounts.

Policies applied to an OU affect:

* All accounts inside that OU
* Any nested OUs and their accounts

This enables **hierarchical governance** across large AWS environments.

---

# Service Control Policies (SCP)

**SCP – Service Control Policy**

Service Control Policies define the **maximum permissions available to AWS accounts within an organization**.

Important principle:

> SCPs **do not grant permissions**.

Instead, they act as **permission guardrails**, restricting what actions accounts are allowed to perform.

Actual permissions must still be granted using **IAM (Identity and Access Management) policies** inside each account.

---

# SCP Inheritance

Service Control Policies are inherited **down the organizational hierarchy**.

```
Root SCP
│
└── Production OU SCP
    │
    └── Member Account
```

Policies applied higher in the hierarchy affect all child Organizational Units and accounts.

This allows administrators to enforce **organization-wide security policies**.

---

# Permission Evaluation

Effective permissions are determined by the **intersection of IAM policies and SCP policies**.

```
IAM Permissions
        ∩
SCP Allowed Permissions
        =
Effective Permissions
```

Only actions allowed by **both** IAM policies and SCP policies can be performed.

---

# Explicit Deny

AWS policy evaluation follows a strict rule:

> **Explicit Deny overrides Allow**

If an action is explicitly denied in either:

* an IAM policy
* or a Service Control Policy (SCP)

the request will be denied.

---

# Default SCP

When an AWS Organization is created, AWS automatically attaches a default policy:

`FullAWSAccess`

This policy allows access to all AWS services unless additional SCP restrictions are applied.

Administrators can replace this with more restrictive policies depending on governance requirements.

---

# Architectural Takeaways

* AWS Organizations enables **centralized governance of multiple AWS accounts**
* Organizational Units allow **hierarchical account grouping**
* Service Control Policies act as **permission guardrails**
* SCPs restrict even the **root user of member accounts**
* Effective permissions are determined by the **intersection of IAM and SCP policies**

---

# References

Concepts reinforced through:

* AWS Documentation
* Adrian Cantrill – AWS Solutions Architect Associate Course
