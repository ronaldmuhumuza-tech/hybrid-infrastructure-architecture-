# AWS Day 02 – Global Infrastructure & VPC Foundations
**Date:** 24 February 2026

---

## Topics Covered
- Regions, 
- Resilience &
-  VPC Basics

---

## Key Concepts
1. AWS Global Infrastructure & Service Scope
WS operates a globally distributed infrastructure connected by a private high-speed backbone network. The core building blocks are:
    * Regions – Independent geographic areas (e.g. ap-southeast-2)
    * Availability Zones (AZs) – Isolated fault domains inside a region
    * Edge Locations – Used for low-latency content delivery and caching

A key learning point today was understanding service scope:
- Global services (e.g. IAM) -> not tied to a region
- Regional services (e.g. EC2, VPC) -> require region selection
- Region selection in the console directly affects architecture decisions

Regions are isolated by design — geographically, politically, and operationally — giving customers control over performance, compliance, and resilience.

2. Resilience Model (Global → Region → AZ)
Resilience in AWS exists at different levels:
    * Globally resilient services – Not dependent on a single region
    * Region-resilient services – Replicated across multiple AZs within one region
    * AZ-resilient services – Require you to deploy across AZs manually
Important realisation:
 - Hardware fails. AZs can fail. Entire AZ can fail.
 - High availability is not automatic — it is architected intentionally.

Distributing workloads across AZs is foundational. Multi-region design is strategic.

3. VPC Foundations
A Virtual Private Cloud (VPC) is a regional, isolated virtual network inside AWS.
Key characteristics:
    * Regionally scoped
    * Private by default
    * Fully configurable
    * Forms the network boundary for resources

This is effectively AWS networking. My CCNA knowledge directly applies here — especially around:
  - CIDR planning
  - Subnetting
  - Traffic control
  - Isolation principles

VPC design is not just configuration — it is architecture.

4. Default VPC vs Custom VPC
Every region has one default VPC with:
    * CIDR: 172.31.0.0/16
    * One /20 subnet per AZ
    * Internet Gateway attached
    * Auto-assigned public IPv4
    * Security Groups & NACLs preconfigured

Strength:
    * Predictable and fast to deploy

Limitation:
    * Limited flexibility and architectural control

Custom VPCs allow:
       * Full CIDR design control
        * Multiple subnets and segmentation
        * More production-ready architecture

Default VPC is convenience.
Custom VPC is engineering.
---

## Architectural Takeaways
        a) Architecture decisions begin at the region level.
        b) Resilience must be deliberately designed — it is not automatic.
        c) Understanding fault domains (Global -> Region -> AZ) is foundational.
        d) Early CIDR planning prevents future scalability and hybrid constraints.
        c) Default setups are for speed; custom design is for maturity.

---

## Questions for Deeper Study
      i) How does AWS technically isolate AZs while keeping latency low?
      ii) What truly happens during a full region outage?
      iii) When is multi-region architecture justified vs over-engineered?
      iv) How do CIDR choices impact hybrid and multi-cloud design later?
      v) What are the trade-offs between simplicity and architectural control in VPC design?
  
