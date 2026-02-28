# AWS Day 05 – Monitoring, Resilience & Route 53 Fundamentals  
**Date:**28 February 2026  
**Focus:** CloudWatch, Shared Responsibility, HA vs FT vs DR, Route 53

---

# 1. CloudWatch Monitoring & Alarm Testing

## Practical Lab

- Created CloudWatch alarms
- Installed stress utility on EC2
- Simulated high CPU utilization
- Observed alarm transition into ALARM state

### Architectural Insight

Monitoring must be **validated**, not assumed.

A resilient system requires:
- Defined thresholds
- Verified alerting mechanisms
- Tested automation

CloudWatch enables:
- Metrics
- Logs
- Alarms
- Event-driven automation

Failure detection is the foundation of resilience.

---

# 2. AWS Shared Responsibility Model

## Core Principle

AWS operates under:

- **Security of the Cloud → AWS responsibility**
- **Security in the Cloud → Customer responsibility**

---

## AWS Responsibility (Security of the Cloud)

AWS manages:

- Physical data centers
- Hardware
- Networking backbone
- Storage infrastructure
- Hypervisor
- Environmental controls
- Physical security

---

## Customer Responsibility (Security in the Cloud)

For EC2 (IaaS), the customer manages:

- Operating system configuration
- Patching & updates
- Application security
- IAM configuration
- Data protection
- Encryption configuration
- Security Groups / network rules
- Monitoring setup

---

## Key Architectural Takeaway

Misconfiguration is usually the customer's responsibility.

Understanding this boundary is critical for:
- Security design
- Compliance
- Risk management

Exam Trap:
A breached database due to weak password policy → Customer responsibility.

---

# 3. High Availability (HA)

## Definition

High Availability aims to **maximize uptime**.

It does NOT mean:
- No failures
- No user disruption

It focuses on:
- Rapid recovery
- Minimal downtime

---

## Availability Levels

| Availability | Downtime per Year |
|--------------|------------------|
| 99.9% (3 nines) | ~8.77 hours |
| 99.99% | ~52.6 minutes |
| 99.999% (5 nines) | ~5.26 minutes |

Downtime includes:
- Detection
- Diagnosis
- Recovery

---

## HA Strategies

- Active–Standby
- Multi-AZ deployments
- Rapid instance replacement
- Automation

HA accepts brief disruption.

---

# 4. Fault Tolerance (FT)

## Definition

Fault Tolerance allows a system to **continue operating properly during component failure**.

Unlike HA:
- No visible interruption
- Operates through failure

---

## Key Distinction

| High Availability | Fault Tolerance |
|------------------|----------------|
| Rapid recovery | Continuous operation |
| Short downtime acceptable | No downtime |
| Lower complexity | Higher complexity |
| Lower cost | Higher cost |

Fault Tolerance requires:
- Active-active systems
- Real-time redundancy
- Complex architecture

Exam Insight:
Most workloads require HA, not full FT.

---

# 5. Disaster Recovery (DR)

## Definition

Disaster Recovery is a structured set of policies and procedures for **recovering after catastrophic failure**.

If HA/FT fail --> DR begins.

---

## Core Elements

- Pre-planned recovery procedures
- Off-site backups
- Defined roles and responsibilities
- Testing and simulations
- Automation where possible

---

## Critical Principle

Never store backups in the same location as primary systems.

Cloud implication:
Use cross-region replication for critical workloads.

---

## HA vs FT vs DR Summary

- HA --> Minimize downtime
- FT --> Operate through failure
- DR --> Recover after catastrophe

---

# 6. Route 53 Fundamentals

## What Is Route 53?

AWS’s managed DNS service.

- Global service
- Highly resilient
- Globally distributed
- Scalable

DNS is hierarchical delegation.

---

## Core Capabilities

1. Domain Registration
2. Hosted Zones (DNS as a Service)

---

## DNS Delegation Flow

1. Create Hosted Zone (zone file)
2. Route 53 allocates 4 managed name servers
3. Zone file loaded onto those servers
4. TLD (Top-Lvel Domain Registry) registry updated with NS (Nameserver) records
5. DNS delegation chain established

Route 53 becomes authoritative for the domain.

---


### Explanation

- **IANA** manages the Root Zone of the global DNS system.
- The Root delegates authority to **TLD registries**.
- The TLD registry delegates to your domain’s **authoritative name servers**.
- Those name servers host your actual **DNS records**.

DNS is a distributed system of hierarchical delegation.
---
## 🧭 DNS Roles – Key Terminology

- **Registry**  
  Manages the official database for a Top-Level Domain (TLD).  
  Example: Verisign for `.com`, PIR for `.org`.

- **Registrar**  
  Acts as the intermediary between customers and the registry.  
  Registers domains and updates the TLD registry with NS records.

- **Authoritative Name Server**  
  Hosts the actual DNS zone file (Hosted Zone in Route 53) and provides DNS answers for that domain.
  ---
  
# 🗂 7. Hosted Zones

A Hosted Zone is a DNS zone file hosted on AWS-managed name servers.

Two types:

## Public Hosted Zone

- Accessible from the internet
- Part of global public DNS system

## Private Hosted Zone

- Linked to one or more VPCs
- Only accessible inside those VPCs
- Used for internal DNS resolution

---

# 8. DNS Record Types (Exam Relevant)

- NS --> Name Servers
- A --> IPv4 address mapping
- AAAA --> IPv6 address mapping
- CNAME --> Alias to another domain name (NOT an IP address)
- MX --> Mail routing
- TXT --> Verification / authorization / anti-spam

Exam Trap:
CNAME records cannot point directly to IP addresses.

---

# 9. DNS TTL (Time To Live)

TTL determines how long DNS records are cached.

Important practice:

Lower TTL **before planned changes** to reduce propagation delays.

Failure to plan TTL changes can cause:
- Extended downtime
- Delayed DNS updates
- Operational confusion

---

# Architectural Day 5 Takeaways

- Monitoring must be tested, not assumed.
- Security boundaries must be clearly understood.
- HA minimizes downtime.
- FT eliminates visible disruption.
- DR ensures survival after catastrophe.
- DNS is hierarchical delegation.
- Public vs Private Hosted Zones define exposure.
- TTL planning is operational discipline.

---
