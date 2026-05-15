---
title: "Week 1: AWS Foundation & Strategic Onboarding"
date: 2026-04-21
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

# Week 1: Comprehensive Cloud Onboarding & Mastering AWS Fundamentals

### I. Executive Summary
The inaugural week of the First Cloud AI Journey (FCJ) Internship served as a critical transition phase. My primary focus was to move beyond basic cloud awareness and establish a professional-grade development environment. This involved not only technical configurations but also aligning with the AWS "Well-Architected Framework" right from day one. By the end of this week, I successfully secured my cloud perimeter and demonstrated technical proficiency by claiming $100 in promotional credits.

### II. Detailed Project Activities & Timeline

| Timeline | Activity Category | Description of Tasks Executed | Deliverables/Artifacts |
| :--- | :--- | :--- | :--- |
| **Day 1-2** | **Onboarding & Security** | Formally joined the FCJ workspace. Implemented high-level security protocols for the root account, including Hardware/Virtual MFA. | Secured AWS Root Account |
| **Day 3** | **Global Infra Research** | Deep-dive into AWS Global Infrastructure. Analyzed the relationship between Regions, Availability Zones (AZs), and Local Zones. | Infrastructure Topology Map |
| **Day 4** | **Environment Setup** | Installed AWS CLI v2, Session Manager Plugin, and configured local profiles. Tested connectivity using STS (Security Token Service). | Functional CLI Environment |
| **Day 5-6** | **Skill Validation** | Participated in intensive "Explore AWS" workshops and executed 5 hands-on labs covering AI, Serverless, and Databases. | **$100 Claimed Credits** |
| **Day 7** | **Documentation** | Structured the Hugo-based internship portfolio and audited initial cost configurations. | Live Worklog Portal |

### III. Technical Deep Dive: The Core Pillars

#### 1. Security & Identity (IAM) - The Perimeter
I implemented a robust IAM strategy to avoid the common mistake of over-privileged accounts:
* **IAM Admin User:** Created a dedicated administrator user, shifting all daily operations away from the Root account.
* **MFA Implementation:** Enforced Multi-Factor Authentication for every sign-in attempt to mitigate credential theft risks.
* **JSON Policies:** Analyzed the structure of IAM policies to understand how `Allow/Deny` statements interact.

#### 2. Service Exploration & The $100 Credit Milestone
To earn the $100 credits, I had to successfully deploy and manage resources across 5 distinct domains:
* **Amazon Bedrock (AI/ML):** Evaluated different Foundation Models (FMs). Practiced invoking models via the playground to understand tokens and response latencies.
* **AWS Lambda (Compute):** Developed a basic serverless function. This shifted my perspective from "managing servers" to "writing logic."
* **Amazon RDS (Database):** Provisioned a relational database. I focused on the "Automated Backup" and "Multi-AZ" features to ensure data durability.
* **Amazon EC2 (Compute):** Launched a T3.micro instance, configured Security Groups (Port 22/80), and accessed it via SSH.
* **AWS Budgets (Governance):** Created a zero-spend budget alert to ensure I stay within the Free Tier limits.

### IV. Challenges, Troubleshooting & Lessons Learned
* **Technical Hurdle:** Encountered an `AccessDenied` error when trying to list S3 buckets via CLI.
* **Root Cause Analysis:** The IAM user lacked the `s3:ListAllMyBuckets` permission.
* **Resolution:** Manually edited the Inline Policy to grant specific S3 permissions, adhering to the "Least Privilege" principle. This was a vital lesson in cloud security.

### V. Professional Reflection
The first week was an eye-opener regarding the scale of AWS. It’s not just about "hosting a website"; it's about building a scalable, secure, and cost-effective ecosystem. Earning the $100 credits was a great practical test of my ability to follow complex technical documentation under time pressure.

### VI. Roadmap for Week 2: The "Deep Dive" Phase
Moving forward, I will focus on the following core labs:
1. **Lab 1:** Advanced IAM and Organizational Units (OU).
2. **Lab 2:** Virtual Private Cloud (VPC) - Designing a custom network topology.
3. **Lab 3:** Elastic Compute Cloud (EC2) - Auto Scaling and Load Balancing.