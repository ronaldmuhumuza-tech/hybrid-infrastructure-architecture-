AWS Learning Log – EC2 Fundamentals & Instance Lifecycle

Date: 25 February 2026
Focus: Amazon EC2, Instance States, Billing & AMIs

1. Amazon EC2 (Elastic Compute Cloud) – Core Concepts
Amazon EC2 (Elastic Compute Cloud) is AWS’s primary Infrastructure as a Service (IaaS) offering. It provides virtual servers (called instances) running inside a Virtual Private Cloud (VPC).

An EC2 instance includes:
  *  vCPU (virtual CPU) – Compute processing power
  *  Memory (RAM) – Working memory for applications
  *  Elastic Block Store (EBS) – Persistent block storage
  *  Networking – Connectivity within the VPC and optionally to the internet

EC2 is:
  -  Regionally scoped
  -  Launched into a specific Availability Zone (AZ)
  -  AZ-resilient only if you deploy across multiple AZs

If the AZ fails --> the instance fails. Single-instance deployments are not highly available.

2. Instance Sizing & Billing Model
EC2 instances come in multiple instance families and sizes, optimised for:
   - General purpose
   - Compute optimised
   - Memory optimised
   - Storage optimised

Billing (On-Demand model):
    * Charged per second (Linux) or per hour (some Windows/older models)
    *  You only pay for what is provisioned and running

Charges include:
  - Compute time (while running)
  - Elastic Block Store (EBS) storage (even when stopped)
  - Data transfer (in certain directions)
  - Commercial software licensing (e.g. Windows Server, SQL Server)

Key billing insight:
            Instance State	    Compute Charged?	    Storage Charged?
                    Running	          Yes	            Yes
                    Stopped	          No	          Yes (EBS still allocated)
                    Terminated	      No	        No (if EBS set to delete)

Only termination guarantees no further charges.

3  EC2 Instance Lifecycle & States
An EC2 instance moves through defined states:
      -> Pending – Launching
      -> Running – Operational
      -> Stopping – Transitioning to stopped
      -> Stopped – Compute resources released
      -> Shutting-down – Being terminated
      -> Terminated – Permanently deleted

Important technical behaviour:
* When stopped, the instance loses: CPU, RAM & Host networking allocation
* But retains: Attached EBS volumes & Private IP address (if within same subnet)
Termination:
  - Deletes the instance
  - By default deletes the root EBS volume (unless configured otherwise)
  - Is irreversible

Exam relevance:
Understanding billing implications of instance state transitions is a common exam theme.

4  Amazon Machine Image (AMI)
An Amazon Machine Image (AMI) is a template used to launch EC2 instances.
It contains:
    -  Boot Volume: Operating system and base software
    -  Block Device Mapping – Configuration describing how storage volumes attach to the instance
    - Launch Permissions – Defines who can use the AMI:
          * Private (owner only)
          * Shared (specific AWS accounts)
          * Public (available to all)

Analogy: An AMI is similar to a VM image on-premises or a bootable OS installer — but is cloud-native.

AMIs allow:
  - Rapid scaling
  - Standardised deployments
  - Reproducible infrastructure
Creating AMIs from configured instances is foundational for scalable architecture.

5  Storage Options – Local vs Elastic
Two storage models:
Instance Store (Local On-Host Storage)
    - Physically attached to the host machine
    - High performance
    - Lost if the instance stops or fails
    - Not persistent

Amazon Elastic Block Store (EBS)
    * Network-attached block storage
    * Persistent
    * Survives instance stop/start
    * AZ-scoped

Important:
EBS volumes exist independently of instance compute lifecycle.

6  Connecting to EC2 Instances
Linux Instances
  - Protocol: SSH (Secure Shell), Port: 22
  - Authentication: Key pair (public/private key cryptography)
    * Public key stored on instance
    * Private key kept securely by user

Tools:
    - Native SSH client
    - PuTTY (on Windows)

Windows Instances
  -  Protocol: RDP (Remote Desktop Protocol), Port: 3389

Authentication:
  - Local Administrator account
  - Encrypted password (retrieved using key pair)

Security Groups must allow inbound access on the appropriate port.

7  Practical Lab Completed
Today I:
  - Launched an EC2 instance
  - Configured Security Groups
  - Deleted the instance

This reinforced:
  - How region and AZ selection matters
  - Security Group configuration controls access
  - Termination behaviour
  - How quickly infrastructure can be provisioned and removed
  - The speed of provisioning compared to on-premises is significant.

*** Architectural Takeaways
    - EC2 is compute only — resilience must be designed (multi-AZ, Auto Scaling, Load Balancing).
    - Billing is tied to lifecycle state — especially important in cost management.
    - Storage persistence (EBS vs Instance Store) changes failure behaviour.
    - AMIs are foundational to scalable, repeatable architecture.
    - Single-instance deployments are not production-grade design.

**** Questions for Deeper Study
  * How does Auto Scaling improve EC2 resilience across Availability Zones?
  * What happens to IP addresses when an instance is stopped vs terminated?
  * What are the security implications of overly permissive Security Groups?
  * How does EC2 placement (Dedicated Hosts, Placement Groups) impact performance?

Personal Reflection
EC2 feels like the bridge between traditional infrastructure and cloud-native thinking.

The biggest mental shift is this: Infrastructure is no longer something you “own.” It is something you define, launch, scale, and destroy intentionally.

The power is flexibility — but the responsibility is architecture.
