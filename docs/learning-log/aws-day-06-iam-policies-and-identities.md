# AWS Day 06 – IAM Policies & Identity Access Model

**Date:** 4 March 2026
**Focus:** IAM Policies, IAM Users, IAM Groups, Authentication & Authorization

---

# 1. IAM Policies – Core Concept

IAM policies define **permissions in AWS**.

They determine **what actions identities can perform on which resources**.

Policies are attached to identities such as:

* IAM Users
* IAM Groups
* IAM Roles

A policy is essentially a **set of security statements** that:

* Allow access
* Deny access

to AWS services and resources.

Policies are also called **Policy Documents** and are written in **JSON**.

---

# 2. Policy Document Structure

An IAM policy document contains **one or more statements**.

Each statement defines a permission rule.

Example structure:

```json
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Effect": "Allow",
     "Action": "s3:ListBucket",
     "Resource": "arn:aws:s3:::example-bucket"
   }
 ]
}
```

Key elements inside a statement include:

| Element   | Purpose                        |
| --------- | ------------------------------ |
| Effect    | Allow or Deny                  |
| Action    | AWS API operation              |
| Resource  | Resource the action applies to |
| Condition | Optional restrictions          |

Understanding how to **read policies** is essential for security troubleshooting.

---

# 3. IAM Permission Evaluation Logic

AWS evaluates permissions using three core rules.

### 1️ Explicit Deny

Always overrides any other permission.

```
Explicit Deny > Allow
```

If a policy contains an explicit deny, access is **blocked immediately**.

---

### 2️. Explicit Allow

Access is granted **only if no explicit deny exists**.

---

### 3️. Implicit Deny (Default)

All identities start with **no permissions**.

This is called **Implicit Deny**.

Unless access is explicitly allowed, it is denied.

Exception:

* **Account Root User** has full permissions.

---

# 4. Types of IAM Policies

There are two main policy types.

---

## Managed Policies (Best Practice)

Managed policies are standalone policy objects that can be attached to multiple identities.

Advantages:

* Reusable
* Easier to maintain
* Centralized management

Two categories exist.

### AWS Managed Policies

Created and maintained by AWS.

Example:

```
AmazonS3ReadOnlyAccess
```

Useful but may not match exact requirements.

---

### Customer Managed Policies

Created by administrators.

Advantages:

* Fully customizable
* Precise permission control
* Recommended for production environments

---

## Inline Policies

Inline policies are embedded directly into a single identity.

Characteristics:

* One-to-one relationship
* Cannot be reused
* Harder to manage

Used only for **special or exceptional cases**.

Best practice: **prefer managed policies**.

---

# 5. IAM Users

An **IAM User** represents an identity that requires long-term access to AWS.

Examples:

* Human users
* Applications
* Service accounts
* Scripts or automation tools

IAM users authenticate using **long-term credentials**.

Examples include:

* Username and password
* Access Keys
* CLI credentials

---

# Long-Term Credentials

IAM users may use **Access Keys** consisting of:

* Access Key ID
* Secret Access Key

These are used by:

* AWS CLI
* SDKs
* Applications running outside AWS

Because they are long-term credentials, they must be **carefully protected and rotated regularly**.

---

# 6. Authentication vs Authorization

Access to AWS resources follows a two-stage process.

### Authentication

The identity proves **who it is**.

Examples:

* Password login
* Access keys
* MFA

---

### Authorization

After authentication, AWS evaluates **IAM policies** to determine:

* What actions are allowed
* Which resources can be accessed

This is called **policy evaluation**.

---

# 7. Amazon Resource Names (ARN)

AWS resources are uniquely identified using **ARNs**.

Example:

```
arn:aws:s3:::example-bucket
```

ARNs allow policies to specify **exact resources or groups of resources**.

---

# 8. IAM Groups

IAM Groups are **containers for IAM users**.

They exist to simplify permission management.

Instead of attaching policies to individual users, policies can be attached to groups.

Example:

```
Developers Group
    ├── Alice
    ├── Bob
    └── Carol
```

All users inherit the group’s permissions.

---

## Key Characteristics of Groups

* Contain IAM users only
* Cannot contain other groups
* Cannot be nested
* Do not have credentials
* Cannot be used as a principal

Groups exist **only for permission organization**.

---

# 9. IAM Limits and Key Facts

| Item                   | Limit              |
| ---------------------- | ------------------ |
| IAM Users per account  | 5,000              |
| IAM Groups per account | 300 (can increase) |
| Groups per user        | 10                 |
| Users per group        | No strict limit    |
| Group nesting          | Not supported      |

For large-scale systems:

* IAM Roles
* Identity Federation

are preferred solutions.

---

# Architectural Insights

* IAM policies define the **security model of AWS environments**.
* Explicit deny always overrides allow.
* Managed policies provide scalable permission management.
* Groups simplify permission assignment for large user populations.
* IAM users should be minimized in modern architectures in favor of **roles and federation**.

Identity is the **foundation of all AWS security design**.
