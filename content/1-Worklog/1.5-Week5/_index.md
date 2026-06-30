---
title: "Week 5: Advanced IAM Governance, Storage Security & Data Encryption"
date: 2026-05-19
weight: 5
chapter: false
pre: "<b> 1.5. </b> "
---

### I. Executive Summary
This week marks a significant milestone in mastering cloud infrastructure, focusing on enterprise-grade identity governance and data security. The content emphasizes applying the Principle of Least Privilege through advanced IAM features such as Permission Boundaries and Resource Tags. Furthermore, the week covers technical operations for enterprise file storage with Amazon FSx and the implementation of At-Rest data encryption strategies using AWS KMS, ensuring compliance with the most stringent security standards in modern cloud environments.

### II. Strategic Objectives
* **IAM Governance:** Master advanced access control mechanisms, including Permission Boundaries and Policy Conditions.
* **Storage Security:** Deploy high-availability, scalable file storage infrastructure using Amazon FSx for Windows.
* **Data Protection:** Build robust data protection pipelines by encrypting S3 objects with AWS KMS and auditing activities via CloudTrail and Athena.
* **Operational Efficiency:** Optimize resource management through Resource Tagging and context-based authorization policies.

### III. Activity Log & Detailed Roadmap (From 19/05/2026 to 25/05/2026)

| Date | Activity Category | Detailed Technical Tasks | Outcome/Proof of Completion |
| :--- | :--- | :--- | :--- |
| **Day 1** *(19/05)* | Enterprise Storage | Deploy Lab 25: Configure Amazon FSx for Windows, set up File Shares, and test performance. | File storage system ready for Active Directory integration. |
| **Day 2** *(20/05)* | S3 Security Basics | Deploy Lab 57: Configure Static Website hosting on S3, set up public access policies, and CloudFront. | Static website globally distributed with low latency. |
| **Day 3** *(21/05)* | IAM & Resource Tags | Deploy Lab 28: Implement access policies based on Resource Tags for EC2 services. | Permissions controlled via resource identification (Tags). |
| **Day 4** *(22/05)* | Permission Boundaries | Deploy Lab 30: Configure IAM Permission Boundaries to isolate administrator scope. | Prevent privilege escalation beyond authorized boundaries. |
| **Day 5** *(23/05)* | Data Encryption | Deploy Lab 33: Configure AWS KMS to encrypt S3 objects and capture logs via CloudTrail/Athena. | Data secured with centralized key management. |
| **Day 6** *(24/05)* | Advanced IAM | Deploy Lab 44: Configure Roles with IP and Time-based Conditions to enhance security. | Access strictly controlled within defined constraints. |
| **Day 7** *(25/05)* | Authorization & Role | Deploy Lab 48: Eliminate Access Keys and migrate to IAM Roles for EC2-hosted applications. | Achieved security standards for EC2-based application authorization. |

### IV. In-depth Technical Execution & Analysis

#### 1. Lab 25: Amazon FSx for Windows File Server

**1. Technical Overview**
Amazon FSx for Windows File Server provides a fully managed file storage system compliant with the SMB (Server Message Block) protocol. It leverages the Windows Server platform, supporting Active Directory, NTFS, and DFS (Distributed File System). This architecture enables seamless migration of Windows-based applications to the cloud without code changes. The service automates backups and maintains high availability, significantly reducing data loss risks for enterprise environments.

**2. Execution Process**
* **Step 1: File System Configuration:** Configured a storage capacity of 32 GiB on SSD to ensure high I/O throughput for demanding tasks.
* **Step 2: Network & Security Governance:** Attaching FSx to the default VPC ensures resource isolation. However, integration with *AWS Managed Microsoft Active Directory* is strictly required for user authentication and file-level access control via standard NTFS permissions.
* **Step 3: Optimization:** Daily automated backups and scheduled maintenance windows are essential configurations to ensure long-term data integrity and system reliability.

**3. Proofs**
* **1.png:** Configuration screen showing technical specifications, SSD capacity selection, and the Active Directory integration requirement.

---

#### 2. Lab 57: Starting with Amazon S3

**1. Technical Overview**
Amazon S3 is an object storage service providing industry-leading scalability, data availability, security, and performance. In this lab, I configured S3 as a static website host, enabling content delivery without the need to manage complex server infrastructure.

**2. Execution Process**
* **Step 1: Storage Setup:** Initialized an S3 Bucket and disabled the Public Access Block to ensure web accessibility.
* **Step 2: Hosting Configuration:** Enabled Static Website Hosting and defined `index.html` as the default homepage.
* **Step 3: Security Governance:** Implemented a Bucket Policy granting `s3:GetObject` permissions to allow public rendering of the website content.

**3. Proofs**
* **2.png:** Configuration screen showing Static Website Hosting successfully enabled.
* **3.png:** Bucket Policy configuration allowing public access for website content.

---

#### 3. Lab 28: Manage access to EC2 services with resource tags through IAM

**1. Technical Overview**
This lab focuses on advanced AWS IAM permission techniques using Conditions. Instead of granting blanket access, I implemented resource-based control via Resource Tags. Only EC2 resources with tags matching the specified policy allow Start/Stop actions, enhancing security and enabling Department-level isolation of resources.

**2. Execution Process**
* **Step 1: Specialized Policy Initialization:** Constructed an IAM Policy using JSON with a `Condition` block to restrict execution permissions based on `aws:ResourceTag/Department`.
* **Step 2: Identity Governance:** Created and configured an IAM Role/User and attached the specialized Policy to manage access to EC2 resources.
* **Step 3: Intelligent Authorization:** Verified that only EC2 instances tagged with `Department: Finance` fall within the scope of this Role's management permissions.

**3. Proofs**
* **4.png:** Configuration screen for the JSON Policy with the `aws:ResourceTag/Department` Condition.
* **5.png:** Detailed Role view after successfully attaching the specialized Policy.

---

#### 4. Lab 30: Limitation of user rights with IAM Permission Boundary

**1. Technical Overview**
Permission Boundary is an advanced IAM security feature that sets a maximum "permission ceiling" for an IAM entity (User or Role). Even if a User is granted AdministratorAccess, they cannot perform actions that exceed the boundaries defined in their associated Permission Boundary. This is a core technique for enforcing the "Least Privilege" principle at scale.

**2. Execution Process**
* **Step 1: Define Boundaries:** Created a Policy to serve as a "Boundary," defining the maximum scope of services accessible to the user (e.g., restricted to S3 management).
* **Step 2: Assign Boundary:** Applied the Permission Boundary to a specific IAM User, ensuring that all future permissions for that user are capped by the pre-defined "ceiling."
* **Step 3: Verification:** Tested granting excessive permissions to the user to confirm that the Boundary successfully blocks unauthorized actions.

**3. Proofs**
* **6.png:** Policy configuration acting as the "Permission Boundary" with specific access restrictions.
* **7.png:** IAM User interface confirming the successful assignment of the Permission Boundary.

---

#### 5. Lab 33: AWS Key Management Service (KMS)

**1. Technical Overview**
AWS KMS is a managed service that makes it easy to create and control cryptographic keys used to encrypt data. In this lab, I created a Customer Managed Key (CMK) to perform data encryption and decryption, and configured separate admin and usage permissions, adhering to the principle of least privilege for key management.

**2. Execution Process**
* **Step 1: Key Initialization:** Created a Symmetric Key for encryption/decryption purposes.
* **Step 2: Key Policy Configuration:** Defined IAM users/roles permitted to manage the key (Key Administrators) and those permitted to use the key (Key Users).
* **Step 3: Encryption Execution:** Used the KMS key to encrypt sample data, verifying the service's security capabilities.

**3. Proofs**
* **8.png:** Confirmation screen showing the successful creation of `Lab33-My-KMS-Key`.
* **9.png:** Output display showing the resulting ciphertext after encryption with the KMS key.

---



### III. Activity Log & Detailed Roadmap (June 22, 2026 – June 30, 2026)

| Time | Activity Category | Specialized Tasks Performed | Results/Proofs Achieved |
| :--- | :--- | :--- | :--- |
| **Day 1** | Enterprise Storage | Deployed Lab 25: Configured Amazon FSx for Windows, setup File Shares, and performance benchmarking. | Windows file storage ready, supporting SMB protocol for the AD environment. |
| **Day 2** | S3 Security Basics | Deployed Lab 57: Static website hosting on S3, public access policy, and CloudFront optimization. | Static website globally distributed with low latency, secured via CDN. |
| **Day 3** | IAM & Tagging | Deployed Lab 28: Established Attribute-Based Access Control (ABAC) using Resource Tags. | Access control governed flexibly based on EC2 instance identifiers (Tags). |
| **Day 4** | Permission Boundary | Deployed Lab 30: Configured IAM Permission Boundary to cap maximum permissions. | Prevented privilege escalation actions outside the designated scope. |
| **Day 5** | Data Encryption | Deployed Lab 33: Configured AWS KMS for data encryption at rest. | Data protected securely with centralized key management and strict control. |

---

### V. Infrastructure Challenges, Error Log & Expert Perspective

* **Challenges:** The primary obstacle in Lab 25 was the mandatory requirement for *AWS Managed Microsoft Active Directory*. The deployment process was costly and time-consuming, requiring careful resource planning.
* **Error Log:** The error message "*AWS Managed Microsoft Active Directory is required*" occurred when initializing FSx without a pre-configured Domain Controller. The solution involved pre-establishing VPC connectivity and Directory identities.
* **Expert Perspective:** FSx for Windows File Server is not just storage; it supports automatic capacity scaling and data backup via AWS Backup, which is ideal for enterprise systems with growing data requirements.
* **Recommendations:** For Linux workloads, I highly recommend using **Amazon EFS** instead of FSx. EFS offers concurrent access for thousands of EC2 instances via the NFS protocol; it is more flexible, eliminates the need for complex Active Directory infrastructure, and significantly reduces the Total Cost of Ownership (TCO).

---

### VI. Professional Reflections

This week brought a major shift in my mindset regarding cloud security. I realized that granting "Administrator" rights is merely a temporary fix, whereas the "Least Privilege" and "Separation of Duties" models are the true keys to operating large-scale systems. Mastering Permission Boundaries and KMS has not only enabled me to identify and mitigate privilege escalation risks but also strengthened my ability to consult on data security solutions, ensuring businesses remain resilient against internal threats.

---

### VII. Strategic Planning & Optimization Roadmap for Next Week

**Strategic Objectives:** Accelerate completion of technical modules, gain hands-on corporate experience, and kick-off the final year capstone project.

**Roadmap:**
1.  **Conquer Modules 6 & 7:** Complete lab exercises for modules 6 and 7 to solidify foundational knowledge of advanced system architectures.
2.  **Office-based Learning:** Maintain the internship schedule at the AWS Vietnam office, maximizing opportunities to engage with experts and observe real-world operational workflows.
3.  **Initiate Capstone Project:** Research and conceptualize the deployment for the "Vietnam Tour Booking Website integrated with Intelligent AI Chatbot" project, focusing on system architecture and data flows.
4.  **Infrastructure Optimization:** Apply learned security techniques to the project, specifically utilizing IAM Roles and Permission Boundaries to safeguard user data.
5.  **Supporting Technology Research:** Deep-dive into Microservices architecture and AI-driven solutions to integrate into real-world applications.