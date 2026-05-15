---
title: "Week 3: Server Deployment and Cloud Storage"
date: 2026-05-05
weight: 3
chapter: false
pre: "<b>3. </b>"
---

This week, I began deploying the core components of a real-world architecture on AWS, including virtual servers (EC2), cloud storage (S3), and relational databases (RDS).

## 4. Lab 4: Amazon EC2 - Virtual Web Server

**Amazon EC2 (Elastic Compute Cloud)** provides scalable computing capacity in the AWS Cloud. Instead of purchasing physical hardware, I can launch a Linux server in minutes.

### Core Concepts:
* **AMI (Amazon Linux 2023):** An AWS-optimized Linux operating system.
* **Instance Type (t2.micro):** Hardware configuration within the Free Tier.
* **Security Group:** A virtual firewall controlling Port 22 (Management) and Port 80 (Web access).
* **User Data:** A script to automatically install Apache Web Server upon instance launch.

### Implementation Process:

#### Step 1: Name and OS Configuration
I named the instance `MyWebServer` and selected Amazon Linux 2023.
![Step 1](/my-hugo-site/images/week3/anh1.png)

#### Step 2: Select Free Tier and Create Key Pair
Used `t2.micro` for cost optimization and created `my-key.pem` for secure login.
![Step 2](/my-hugo-site/images/week3/anh2.png)

#### Step 3: Network Settings (VPC & Subnet)
The instance was placed in the pre-configured `MyLabVPC`, using a Public Subnet with Public IP enabled. Security Group was configured to allow HTTP traffic.
![Step 3](/my-hugo-site/images/week3/anh3.png)

#### Step 4: Automation Script (User Data)
Injected a shell script to automate the environment setup and web server installation.
![Step 4](/my-hugo-site/images/week3/anh4.png)

#### Step 5: Instance Status Check
The system confirmed the instance is **Running** and passed all status checks (2/2 checks passed).
![Step 5](/my-hugo-site/images/week3/anh5.png)

#### Step 6: Live Access via Public IP
Accessed the web server's Public IP through a browser to verify the deployment.
![Step 6](/my-hugo-site/images/week3/anh6.png)

---
*Future labs regarding Lab 5 (S3) and Lab 6 (RDS) will be updated in upcoming sessions.*