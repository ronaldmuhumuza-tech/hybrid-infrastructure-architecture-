# AWS Day 06.2 – Service-Linked Roles and AWS STS

**Date:** 5 March 2026
**Topics:** Service-Linked Roles, iam:PassRole Permission, STS (Security Token Service)

---

# Service-Linked Roles

## What is a Service-Linked Role?

A **Service-Linked Role (SLR)** is a special **IAM (Identity and Access Management) role** that is tightly integrated with a specific AWS service.

It allows the service to perform actions in your AWS account **on your behalf**.

The permissions assigned to a service-linked role are predefined by AWS and are designed specifically for the service that uses it.

Examples of AWS services that use service-linked roles include:

* Amazon EC2 Auto Scaling
* Elastic Load Balancing
* Amazon RDS (Relational Database Service)
* AWS Lambda

---

# Service-Linked Role Architecture

```text
AWS Service
    │
    └── Assumes
            ↓
      Service-Linked Role
            │
            └── Permissions to interact with other AWS services
```

Example:

Amazon EC2 Auto Scaling may require permissions to:

* Launch EC2 (Elastic Compute Cloud) instances
* Attach Elastic Load Balancers
* Modify Auto Scaling groups

The service-linked role allows the service to perform these actions securely.

---

# Key Characteristics

Service-linked roles have several defining characteristics:

* They are **linked to a specific AWS service**
* Permissions are **predefined and managed by AWS**
* They are often **automatically created** when enabling a service
* They **cannot be deleted while the service still requires them**
* The **trust policy allows only the associated service to assume the role**

This ensures services have the permissions they need without requiring administrators to manually configure complex IAM policies.

---

# iam:PassRole Permission

The IAM permission:

`iam:PassRole`

allows an identity (such as an IAM user or IAM role) to **pass an IAM role to an AWS service**.

Example scenario:

A developer launches an EC2 instance and attaches an IAM role to that instance.

Without the `iam:PassRole` permission, the user cannot attach the role to the EC2 instance.

---

# Why iam:PassRole Matters

The `iam:PassRole` permission is critical for preventing **privilege escalation**.

If it is not properly restricted, a user could attach a highly privileged role to a resource they control.

Example risk:

A developer could attach an **Administrator role** to an EC2 instance.

The EC2 instance would then inherit full administrative permissions.

For this reason, `iam:PassRole` permissions should always be **restricted to specific roles and services**.

---

# AWS STS – Security Token Service

**AWS STS (Security Token Service)** provides **temporary security credentials** that allow access to AWS resources.

Temporary credentials include:

* Access Key ID
* Secret Access Key
* Session Token

These credentials automatically expire after a defined period of time.

Temporary credentials are widely used for:

* Assuming IAM roles
* Identity federation
* Secure short-term access to AWS resources

Because they expire automatically, temporary credentials are **more secure than long-term access keys**.

---

# Role Assumption Flow

```text
Identity (User / Application / AWS Service)
        │
        └── Assume Role
                ↓
        AWS STS (Security Token Service)
                ↓
        Temporary Security Credentials
                ↓
        Access AWS Resources
```

This mechanism allows AWS to issue secure short-lived credentials rather than relying on permanent credentials.

---

# Architectural Takeaways

* Service-linked roles allow AWS services to perform actions **within your account**
* Permissions for service-linked roles are **managed by AWS**
* `iam:PassRole` allows identities to assign roles to AWS services
* Improper `iam:PassRole` configuration can lead to **privilege escalation**
* AWS STS provides **temporary credentials** that improve overall security
* Temporary credentials are preferred over **long-term access keys**

---

# References

Concepts reinforced through:

* AWS Documentation
* Adrian Cantrill – AWS Solutions Architect Associate Course
