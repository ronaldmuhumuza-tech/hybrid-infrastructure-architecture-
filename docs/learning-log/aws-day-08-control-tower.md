# AWS Day 07.3 – AWS Control Tower and Multi-Account Governance

**Date:*13/03/2025*  
**Topic:** AWS Control Tower, Landing Zones, Guardrails, Account Factory

---

# Overview

AWS Control Tower is a service designed to help organizations quickly set up and govern a **secure multi-account environment** in Amazon Web Services (AWS).

It builds on top of **AWS Organizations** and orchestrates several AWS services to create a standardized **Landing Zone** architecture.

Control Tower simplifies:

- Multi-account governance
- Security and compliance
- Centralized identity management
- Automated account provisioning
- Organizational monitoring and auditing

It essentially provides **AWS Organizations with additional governance and automation capabilities**.

---

# Core AWS Services Used by Control Tower

AWS Control Tower integrates multiple AWS services to create a fully governed environment.

Key services include:

- **AWS Organizations**
- **AWS Identity and Access Management (IAM) Identity Center** (formerly AWS Single Sign-On)
- **AWS CloudTrail**
- **Amazon CloudWatch**
- **AWS Config**
- **Amazon Simple Notification Service (Amazon SNS)**
- **AWS CloudFormation**
- **AWS Service Catalog**

Control Tower orchestrates these services to implement governance and operational automation across multiple AWS accounts.

---

# Landing Zone Concept

A **Landing Zone** is a preconfigured multi-account environment built using AWS best practices.

The landing zone includes:

- Identity management
- Security monitoring
- Centralized logging
- Governance guardrails
- Account provisioning automation

When deploying Control Tower, you must select a **Home Region**.

The home region is:

- The region where Control Tower is deployed
- The region where the landing zone is primarily managed

Other regions can be explicitly allowed or restricted.

---

# Control Tower Architecture

Control Tower is deployed within a **Management Account**.

This account becomes the top-level administrative account for the organization.

The architecture includes:

Management Account  
│  
├── AWS Control Tower  
├── AWS Organizations  
├── IAM Identity Center (SSO)  
└── Landing Zone Configuration

Control Tower orchestrates these components to manage multiple AWS accounts securely.

---

# Organizational Units (OU)

AWS Organizations organizes accounts into **Organizational Units (OU)**.

Control Tower automatically creates two default OUs.

---

## Security Organizational Unit

The **Security OU** is a foundational OU designed for governance and auditing.

Two important accounts are created here.

### Log Archive Account

The Log Archive Account stores centralized logs for the entire organization.

Examples of logs stored here include:

- AWS CloudTrail logs
- AWS Config logs

Purpose:

- Secure storage of logging data
- Restricted access for security teams
- Tamper-resistant audit trail

---

### Audit Account

The Audit Account provides access for security teams and auditing tools.

Typical uses include:

- Running security assessments
- Monitoring governance compliance
- Integrating third-party security tools

Monitoring services such as **Amazon CloudWatch** and **Amazon SNS** can be used here for organization-wide alerts.

---

## Sandbox Organizational Unit

The **Sandbox OU** is used for experimentation and testing.

Characteristics:

- Less restrictive governance
- Safe environment for development and experimentation

Organizations can create additional OUs to match their operational structure.

Example organizational model:

Production OU  
Development OU  
Security OU  
Sandbox OU

---

# Identity and Access Management

Control Tower uses **IAM Identity Center (formerly AWS Single Sign-On)** to manage access.

This enables **Single Sign-On (SSO)** across all AWS accounts within the landing zone.

Benefits include:

- One login for multiple AWS accounts
- Centralized permission management
- Identity federation with corporate directories

Identity federation allows integration with external identity providers such as:

- Microsoft Active Directory
- Azure Active Directory
- Okta
- Other Security Assertion Markup Language (SAML) providers

---

# Centralized Monitoring and Logging

Control Tower provides centralized monitoring and auditing using multiple AWS services.

These include:

**AWS CloudTrail**

Records API activity across accounts.

**Amazon CloudWatch**

Monitors metrics and logs.

**AWS Config**

Tracks configuration changes in AWS resources.

**Amazon Simple Notification Service (SNS)**

Sends alerts and notifications.

These services ensure security teams can monitor activity across the entire organization.

---

# Guardrails

Guardrails are governance rules applied across AWS accounts within the landing zone.

They enforce security and compliance policies.

Guardrails fall into three categories.

---

## Mandatory Guardrails

Mandatory guardrails are automatically applied and cannot be disabled.

They enforce essential security standards.

---

## Strongly Recommended Guardrails

These guardrails are recommended by AWS but can be disabled if necessary.

They represent best practices for security and governance.

---

## Elective Guardrails

Elective guardrails are optional and provide additional governance controls.

They allow organizations to implement specialized policies.

---

# Guardrail Enforcement Types

Guardrails operate in two ways.

---

## Preventative Guardrails

Preventative guardrails actively block actions that violate policies.

They are implemented using **Service Control Policies (SCPs)** within AWS Organizations.

Examples:

- Prevent use of specific AWS regions
- Prevent modification of certain security policies
- Restrict creation of specific resource types

Preventative guardrails enforce compliance **before a violation occurs**.

---

## Detective Guardrails

Detective guardrails monitor resources for compliance violations.

They are implemented using **AWS Config Rules**.

Examples:

- Detect whether CloudTrail logging is enabled
- Identify resources without encryption
- Detect EC2 instances with public IPv4 addresses

Detective guardrails do not block actions but instead **report violations**.

---

# Account Factory

Account Factory is an automation feature used to create and manage AWS accounts.

It enables **automated account provisioning**.

Accounts can be created by:

- Cloud administrators
- Authorized end users

Provisioned accounts automatically receive:

- Baseline security configurations
- Networking settings
- Governance guardrails

This ensures consistency across all AWS accounts.

---

# Standardized Account Configuration

Account Factory applies standard configurations during account creation.

Examples include:

- Preconfigured Virtual Private Cloud (VPC) settings
- Standard network address ranges
- Guardrail policies
- Logging configurations

This prevents configuration drift and ensures consistent architecture across the organization.

---

# Integration with CloudFormation

AWS Control Tower uses **AWS CloudFormation** under the hood to automate infrastructure deployment.

CloudFormation stacks are created to configure:

- Accounts
- Policies
- Guardrails
- Monitoring

This enables repeatable and automated environment setup.

---

# Service Catalog Integration

Account provisioning can also be done using **AWS Service Catalog**.

This enables:

- Self-service account creation
- Governance approval workflows
- Integration with development processes

Service Catalog allows Control Tower to integrate with an organization's **Software Development Lifecycle (SDLC)**.

---

# Control Tower Dashboard

Control Tower provides a centralized dashboard that displays:

- Organization health
- Guardrail compliance
- Account status
- Security alerts

This dashboard gives administrators a **single view of the entire AWS environment**.

---

# Key Exam Concepts

For the AWS Solutions Architect Associate exam remember:

AWS Control Tower:

- Builds a **multi-account landing zone**
- Uses **AWS Organizations for account structure**
- Uses **IAM Identity Center for Single Sign-On**
- Provides **centralized logging and monitoring**
- Uses **Guardrails for governance**
- Uses **Account Factory for automated account creation**

Guardrail types:

- Mandatory
- Strongly recommended
- Elective

Guardrail enforcement:

- Preventative → implemented with Service Control Policies
- Detective → implemented with AWS Config Rules

---

# Summary

AWS Control Tower simplifies the creation and governance of multi-account AWS environments.

It provides:

- Automated account provisioning
- Centralized security monitoring
- Governance guardrails
- Identity federation
- Organizational visibility

By combining AWS Organizations with multiple AWS governance services, Control Tower enables organizations to deploy secure and scalable cloud environments quickly.
