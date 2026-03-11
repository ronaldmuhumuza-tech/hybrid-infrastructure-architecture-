# AWS Day 07.2 – AWS CloudTrail

**Date:11/03/2026**  
**Topic:** AWS CloudTrail – Auditing and API Activity Logging

---

# Overview

AWS CloudTrail is a service that records **Application Programming Interface (API) activity across an Amazon Web Services (AWS) account**.

CloudTrail provides visibility into actions performed by:

- Users
- Roles
- AWS services
- Applications

Each recorded action is called a **CloudTrail Event**.

CloudTrail is primarily used for:

- Security auditing
- Compliance monitoring
- Troubleshooting
- Operational visibility
- Forensic investigations

It enables organisations to track **who did what, when, and from where** within an AWS environment.

---

# What is a CloudTrail Event?

A **CloudTrail Event** represents a single activity within an AWS account.

Examples include:

- Creating an **Amazon Elastic Compute Cloud (Amazon EC2)** instance
- Deleting an **Amazon Simple Storage Service (Amazon S3)** bucket
- Logging into the AWS Management Console
- Modifying an **AWS Identity and Access Management (IAM)** policy
- Invoking an **AWS Lambda** function

CloudTrail records these actions as structured log entries.

---

# Default CloudTrail Behaviour

CloudTrail is **enabled by default** in all AWS accounts.

However, the default configuration only provides limited functionality.

---

# CloudTrail Event History

Every AWS account includes **CloudTrail Event History**.

Characteristics:

- Automatically enabled
- Free of charge
- Stores the **last 90 days** of activity
- Records **management events only**

Event History allows engineers to quickly view recent account activity without additional configuration.

However, Event History does not provide **long-term log storage**.

To extend logging capabilities, a **Trail** must be created.

---

# What is a Trail?

A **Trail** is the configuration component used by CloudTrail.

A trail defines:

- What events are captured
- Which AWS regions are monitored
- Where logs are stored

Trails enable:

- Long-term storage of activity logs
- Integration with monitoring systems
- Centralised auditing across multiple regions

---

# CloudTrail Event Types

CloudTrail records three types of events.

---

# 1. Management Events

Management events record **changes to AWS infrastructure resources**.

These are also known as **Control Plane Operations**.

Examples include:

- Creating or terminating EC2 instances
- Creating Virtual Private Clouds (Amazon VPC)
- Modifying security groups
- Creating or deleting S3 buckets
- IAM user login activity

Management events are:

- Enabled by default
- Included in Event History
- Captured by Trails

These events describe **configuration changes to AWS resources**.

---

# 2. Data Events

Data events record **operations performed within AWS resources**.

Examples include:

- Uploading an object to Amazon S3
- Accessing or downloading an S3 object
- Invoking an AWS Lambda function

Data events are:

- Not enabled by default
- Higher volume than management events
- Charged separately

Because operations such as object reads can occur extremely frequently, logging them can generate very large log volumes.

---

# 3. Insight Events

Insight events detect **abnormal patterns in API activity**.

Examples include:

- Sudden increases in API call rates
- Unusual activity patterns

CloudTrail Insights helps identify:

- Potential security threats
- Misconfigured applications
- Unexpected operational behaviour

---

# CloudTrail Region Behaviour

CloudTrail is a **regional service**.

When creating a trail, two configurations are possible.

---

# Single Region Trail

A **single region trail** records events only in the region where it was created.

Example:

If a trail is created in:

eu-west-1

It will only capture events occurring in that region.

---

# Multi-Region Trail

A **multi-region trail** captures events from **all AWS regions**.

Benefits include:

- Centralised monitoring
- Automatic inclusion of newly created AWS regions

Multi-region trails are considered **best practice** for production environments.

---

# Global Service Events

Some AWS services operate as **global services**.

Examples include:

- AWS Identity and Access Management (IAM)
- AWS Security Token Service (STS)
- Amazon CloudFront

These services log their CloudTrail events in:

us-east-1 (Northern Virginia)

These logs are called **Global Service Events**.

A trail must have **global service event logging enabled** to capture them.

---

# CloudTrail Log Storage

CloudTrail logs are typically stored in:

**Amazon Simple Storage Service (Amazon S3)**.

Characteristics:

- Logs are stored as compressed **JavaScript Object Notation (JSON)** files
- Storage is highly cost efficient
- Logs can be retained indefinitely

Typical storage structure:

S3 Bucket  
└── AWSLogs  
    └── AccountID  
        └── CloudTrail

This allows organisations to maintain long-term audit records.

---

# CloudTrail and CloudWatch Integration

CloudTrail logs can also be delivered to:

**Amazon CloudWatch Logs**

Benefits include:

- Real-time monitoring
- Log searching
- Metric filters
- Automated alarms

Example workflow:

CloudTrail  
↓  
Amazon S3 (long-term storage)  
↓  
Amazon CloudWatch Logs  
↓  
Metric Filters  
↓  
CloudWatch Alarms

This integration enables automated detection of suspicious activity.

---

# AWS Organizations Integration

CloudTrail supports **Organization Trails**.

These trails are created from the **management account** of **AWS Organizations**.

An organization trail collects events from:

- All AWS accounts within the organization

Benefits include:

- Centralised security monitoring
- Simplified compliance auditing
- Visibility across multi-account environments

---

# Key Exam Points

For the **AWS Solutions Architect Associate** exam remember:

CloudTrail:

- Records **API activity**
- Is **enabled by default**
- Provides **90-day Event History**
- Requires a **Trail for long-term logging**

Event types include:

- Management Events (default)
- Data Events (optional)
- Insight Events (anomaly detection)

Logs can be stored in:

- Amazon S3
- Amazon CloudWatch Logs

Global service events (IAM, STS, CloudFront) are recorded in:

us-east-1

---

# Summary

AWS CloudTrail is the primary auditing service within AWS.

It records API activity across an AWS account and provides critical visibility for:

- Security monitoring
- Compliance auditing
- Operational troubleshooting

By storing logs in Amazon S3 and integrating with Amazon CloudWatch, CloudTrail enables organisations to build secure and observable cloud environments.
