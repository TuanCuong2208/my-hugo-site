---
title: "Week 2: Architectural Foundations & Core Services"
date: 2026-04-28
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

# Week 2: Mastering AWS Infrastructure - From Identity to Networking

### I. Executive Summary
Week 2 marks the critical transition from initial account onboarding to core infrastructure engineering. The focus of this week is twofold: establishing a "Zero Trust" security model using AWS IAM and designing a logically isolated virtual network via Amazon VPC. These components form the "bedrock" of any scalable cloud architecture.

### II. Strategic Weekly Objectives
* **IAM Hardening:** Shifting from Root-user dependency to a structured, policy-driven administrative environment.
* **Network Virtualization:** Constructing a Virtual Private Cloud (VPC) with high-availability considerations.
* **Operational Excellence:** Maintaining a clean environment by implementing a strict resource lifecycle (Create-Verify-Terminate) to optimize costs.

### III. In-Depth Technical Execution

#### 1. Lab 1: Introduction to AWS Global Infrastructure
Before executing technical labs, I conducted a deep dive into how AWS manages its physical presence. 
* **Regions:** Geographic areas that host multiple Availability Zones. I selected `us-east-1` (N. Virginia) due to its maturity and wide service availability.
* **Availability Zones (AZs):** Distinct data centers with redundant power and networking. I learned that designing for high availability requires distributing resources across multiple AZs to prevent single-point-of-failure (SPOF).

#### 2. Lab 2: IAM Access Control - Security Deep Dive
The objective was to implement the **Principle of Least Privilege (PoLP)**.
* **JSON Policy Dissection:** I analyzed the structure of IAM Policies. I learned that every policy consists of statements including `Effect` (Allow/Deny), `Action` (API calls like `s3:ListBucket`), and `Resource` (The specific ARN of the asset).
* **IAM User Configuration:** Created a dedicated Admin user to act as my daily operator.
![User Configuration](images/week2/iam-create-user-step1.png)
* **Security Dashboard:** Successfully activated MFA for both Root and IAM accounts. The dashboard now shows 100% compliance with AWS security recommendations.
![IAM Dashboard](images/week2/iam-dashboard.png)

#### 3. Lab 3: Virtual Private Cloud (VPC) - The Network Skeleton
Building a VPC is like building a private data center on the cloud.
* **CIDR Block Strategy:** I utilized the `10.0.0.0/16` range, providing 65,536 private IP addresses. This provides enough headroom for future scaling and subnetting.
* **Public Subnet Architecture:** I configured 1 Public Subnet associated with an **Internet Gateway (IGW)**. This IGW acts as a bridge between the VPC and the public internet.
![VPC Architecture](images/week2/vpc-architecture.png)
* **Routing Logic:** I updated the **Route Table** to include a default route (`0.0.0.0/0`) pointing to the IGW, enabling internet connectivity for resources within the subnet.
![VPC Success](images/week2/vpc-create-success.png)

### IV. Challenges, Troubleshooting & Professional Insights
* **The "Hidden Cost" of NAT Gateways:** During the setup, I noted that AWS defaults to creating NAT Gateways. I manually selected "None" to avoid unnecessary costs while still achieving my lab goals using direct IGW routing.
* **Stateless vs. Stateful:** I researched the difference between Security Groups (Stateful) and NACLs (Stateless), deciding to focus on Security Groups for instance-level protection in the next phase.

### V. Professional Reflection
Understanding how a packet travels from the Internet Gateway, through a Route Table, and into a Subnet is the most empowering skill I've learned this week. Cloud engineering is not about "magic"—it is about precise configuration and intentional design.

### VI. Roadmap for Week 3: Core Services & Database Integration
In the upcoming week, I will focus on deploying functional workloads by integrating compute, storage, and database services:
* **Lab 4: Amazon EC2 (Elastic Compute Cloud):** Launching Linux instances, managing Key Pairs, and configuring Security Groups for web access.
* **Lab 5: Amazon S3 (Simple Storage Service):** Exploring object storage, static website hosting, and bucket policy management.
* **Lab 6: Amazon RDS (Relational Database Service):** Deploying managed MySQL/PostgreSQL databases and connecting them to EC2 instances.