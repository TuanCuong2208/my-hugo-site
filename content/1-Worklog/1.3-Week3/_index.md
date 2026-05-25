---
title: "Week 3: Deploying Cloud Servers and Storage"
date: 2026-05-05
weight: 3
chapter: false
pre: "<b>1.3. </b>"
---

During this week, I began deploying the main components of a real-world system on AWS, including virtual servers (EC2), cloud storage (S3), and relational databases (RDS).

## 1. Lab 4: Amazon EC2 - Virtual Web Server

The **Amazon EC2 (Elastic Compute Cloud)** service allows users to rent virtual servers in the cloud. Instead of purchasing physical hardware, I was able to launch a Linux server within minutes.

### Core Concepts:
* **AMI (Amazon Linux 2023):** An operating system optimized for AWS environments.
* **Instance Type (t2.micro):** A hardware configuration included in the AWS Free Tier.
* **Security Group:** A virtual firewall controlling port 22 (administration) and port 80 (web access).
* **User Data:** A startup script that automatically installs the Apache Web Server when the instance launches.

### Implementation Process:

#### Step 1: Configure Server Name and Operating System
I named the server `MyWebServer` and selected Amazon Linux 2023.
![Step 1](/my-hugo-site/images/week3/anh1.png)

#### Step 2: Choose Free Tier Configuration and Create a Key Pair
I selected the `t2.micro` instance type to optimize costs and created the `my-key.pem` file for secure login.
![Step 2](/my-hugo-site/images/week3/anh2.png)

#### Step 3: Configure Networking (VPC & Subnet)
The server was deployed inside the previously created `MyLabVPC`, assigned to a Public Subnet, and configured with a Public IP address. I also configured the Security Group to allow HTTP traffic on port 80.
![Step 3](/my-hugo-site/images/week3/anh3.png)

#### Step 4: Add the Automation Script (User Data)
I inserted a startup script to automatically install and configure the web server environment during launch.
![Step 4](/my-hugo-site/images/week3/anh4.png)

#### Step 5: Verify the Server Status
The system confirmed that the server was running successfully and had passed all health checks.
![Step 5](/my-hugo-site/images/week3/anh5.png)

#### Step 6: Access the Server via Public IP
I used the server’s Public IP address to access the website directly from a web browser.
![Step 6](/my-hugo-site/images/week3/anh6.png)

---

## 2. Lab 5: Amazon S3 - Static Website Hosting

**Amazon S3 (Simple Storage Service)** is a highly scalable and durable object storage service. In this lab, I configured an S3 Bucket to host a static website.

### Core Concepts:
* **S3 Bucket:** A globally unique container for storing objects.
* **Static Website Hosting:** A feature that serves HTML, CSS, and JavaScript files directly from S3.
* **Bucket Policy:** A JSON-based permission configuration that allows public read access.

### Implementation Process:

#### Step 1: Create the Bucket and Enable Public Access
I created a bucket named `cuong-static-website-2026` and unchecked "Block all public access" to prepare the bucket for public website hosting.
![Step 7](/my-hugo-site/images/week3/anh7.png)

#### Step 2: Enable Static Website Hosting
In the Properties tab, I enabled Static Website Hosting and configured `index.html` as the default document.
![Step 8](/my-hugo-site/images/week3/anh8.png)

#### Step 3: Configure the Bucket Policy
I added a JSON policy to grant `s3:GetObject` permission for all internet users.
![Step 9](/my-hugo-site/images/week3/anh9.png)

#### Step 4: Verify the Result
I uploaded the `index.html` file and accessed the website through the endpoint provided by AWS.
![Step 10](/my-hugo-site/images/week3/anh10.png)
![Step 11](/my-hugo-site/images/week3/anh11.png)

---

## 3. Lab 6: Amazon RDS - Relational Database Service

**Amazon RDS** simplifies the setup and management of relational databases in the cloud. In this lab, I deployed a MySQL database instance to support application data storage.

### Core Concepts:
* **DB Engine:** The selected database management system (MySQL).
* **Sandbox (Free Tier):** A cost-optimized configuration template designed for learning and testing.
* **Endpoint:** The database server address used by backend applications for connection.

### Implementation Process:

#### Step 1: Select the Engine and Sandbox Template
I selected MySQL and chose the **Sandbox** template to ensure the configuration remained within the AWS Free Tier limits.
![Step 12](/my-hugo-site/images/week3/anh12.png)

#### Step 2: Launch the Database Instance
I configured the VPC settings and enabled Public Access before launching the database server.
![Step 13](/my-hugo-site/images/week3/anh13.png)

#### Step 3: Verify the Database Status and Endpoint
After the database status changed to **Available**, I retrieved the Endpoint information for future application connections.
![Step 14](/my-hugo-site/images/week3/anh14.png)