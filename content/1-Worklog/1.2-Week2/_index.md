---
title: "Week 2: Architectural Foundations & Core Services"
date: 2026-04-28
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---


### I. Executive Summary
This week marks a strategic and comprehensive turning point in the internship roadmap. I have completely shifted from surface-level conceptual understanding to directly designing, configuring, and mastering the most foundational infrastructure pieces on the AWS cloud ecosystem. The research content spans across 6 major Labs: from surveying the global physical infrastructure, tightening identity security with IAM, planning logically isolated virtual networks with VPC, to directly deploying the core service trio that constitutes a real-world application: Compute servers (EC2), Object storage systems (S3), and Managed relational databases (RDS).

### II. Strategic Objectives of the Week
* **Tightening Identity Security (IAM Security):** Fully realize the "Zero Trust" security model, completely isolating the supreme Root account and establishing a daily operational environment based on the Principle of Least Privilege (PoLP).
* **Virtualizing Network Infrastructure (VPC Engineering):** Personally design and plan a logically isolated virtual network area, mastering routing mechanisms, Subnet partitioning, and inbound/outbound Internet data flow management.
* **Mastering Compute and Storage Resources (Core Infrastructure):** Deploy, operate, and optimize the core service trio: EC2 (Compute), S3 (Storage), and RDS (Database) under a standardized model.
* **Optimizing Operational Costs (FinOps Integration):** Establish a strict resource lifecycle management mindset (Create - Verify results - Terminate dependent resources), completely eliminating the risk of unexpected cost generation on Sandbox accounts.

---

### III. Activity Log & Detailed Allocation Roadmap (From April 28, 2026 to May 4, 2026)

| Time | Activity Category | Detailed In-Depth Tasks Performed | Achievements/Evidence Obtained |
| :--- | :--- | :--- | :--- |
| **Days 1-2** *(Apr 28-29)* | Integration & Security | Surveyed AWS's global physical distributed architecture. Deployed advanced authorization configurations, isolated the Root account, and set up an IAM Admin User. | Root account is multi-layer protected by Virtual MFA, IAM Admin is ready for operation. |
| **Day 3** *(Apr 30)* | Network Virtualization | Planned internal network structure, initiated Virtual Private Cloud (VPC), allocated Public Subnet addresses, established Internet Gateway, and customized Route Table. | A complete logically isolated virtual network system, ready for packet routing. |
| **Day 4** *(May 01)* | Virtual Servers | Executed Linux virtual server launch workflow, configured inbound Security Group firewall, configured User Data encryption to automate Apache Web Server installation. | Server responds smoothly through direct access via Public IP address. |
| **Day 5** *(May 02)* | Cloud Storage | Initiated a globally unique S3 Bucket, removed default block public access mechanisms, configured Bucket Policy via JSON code, uploaded static source code. | Static website is distributed globally on a large scale via AWS Endpoint link. |
| **Day 6** *(May 03)* | Database | Initiated a MySQL Server relational database instance via Amazon RDS, controlled minimum hardware configurations with gp3 and db.t3.micro to maintain Free Tier standards. | Database transitioned to Available state, successfully extracted connection Endpoint. |
| **Day 7** *(May 04)* | Documentation & FinOps | Consolidated entire error log (RDS UI bug, IAM Policy), reviewed and cleaned up dependent resources, packaged Portfolio report on Hugo platform. | Completed a sequential and clean Work Log Portal structure. |

---

### IV. In-Depth Technical Execution & Detailed Analysis via 6 Labs

#### **LAB 1: Introduction to AWS Global Infrastructure**

##### **1. Overview**
Before getting hands-on with configuring complex technical entities, understanding how AWS distributes physical resources on a global scale is mandatory. This research project helps shape the architectural mindset to ensure High Availability, limitless Scalability, and Fault Tolerance.

##### **2. Core Concepts**
* **AWS Regions:** Completely independent geographic locations around the world, designed to comply with strict data sovereignty regulations and minimize latency for end-users. Throughout the Lab series, I prioritized choosing the **`us-east-1` (N. Virginia)** region because it is the central core region of AWS, offers the most optimal cost, and is always updated earliest with new technical features.
* **Availability Zones - AZs:** Each Region will include multiple distinct AZs (minimum of 3). Each AZ is constituted from one or more massive physical data centers, equipped with redundant power, cooling systems, and interconnected via an ultra-low latency fiber-optic network.
* **Single Point of Failure (SPOF) Mindset:** I am deeply aware that deploying the entire application on a single AZ is a fatal mistake. When designing a system, it is mandatory to distribute resources (such as servers or databases) to run concurrently across at least 2 different AZs. If one physical data center encounters a physical disaster (natural disasters, widespread power outage), traffic flow will immediately be redirected to the remaining AZ, ensuring the system is not disrupted.

##### **3. Results Obtained & Professional Analysis**
* Mastered the skill of selecting optimal Regions based on three core parameters: End-user location (reducing latency), National legal compliance, and Pricing of each service type.
* Successfully built a tiered infrastructure mind map: `AWS Global` $\rightarrow$ `Regions` $\rightarrow$ `Availability Zones` $\rightarrow$ `Edge Locations` (Serving the CloudFront CDN content delivery network).

---

#### **LAB 2: AWS IAM Access Control - Setting up a Multi-Layered Security Foundation**

##### **1. Overview**
Security is always the highest priority in the cloud environment under the Shared Responsibility Model. This Lab focuses on realizing the **Zero Trust** cybersecurity model through the AWS Identity and Access Management (IAM) service, tightening all system entry points, and completely preventing the risk of administrative credential leaks.

##### **2. Core Concepts**
* **Principle of Least Privilege (PoLP):** This is the guiding compass in cloud administration. Every entity (user, application, server) is granted only the exact and sufficient minimal permissions required to complete their designated tasks.
* **The Danger of the Root-user:** The Root account (created with the initial registration email) holds the ultimate life-or-death power over the infrastructure, including deleting the account and changing billing information. Therefore, the absolute, unalterable rule is: **Isolate the Root account, lock it away, and never use it for daily configuration tasks.**
* **JSON Policy Structure:** The nature of all authorization on AWS is defined through JSON documents. I dissected a standard IAM Policy and mastered its 4 mandatory components:
  * `Effect`: Determines the selection state (`Allow` or `Deny`).
  * `Action`: The exact API calls allowed or blocked by the system (e.g., `ec2:RunInstances`, `s3:CreateBucket`).
  * `Resource`: The ARN (Amazon Resource Name) that precisely identifies the absolute resource affected by this policy.
  * `Condition` (Optional): The attached bounding conditions (e.g., Only allowing access if the IP originates from the company corporate network, or within a specific time frame).

##### **3. Step-by-step Execution**
1. Log in to the AWS Console using the supreme Root account, search for and access the **IAM** service dashboard.
2. Navigate to **Users** > Select **Create user**. Proceed to initialize a dedicated user account named `Admin-Cuong`.
3. At the permission setup step (Set permissions), I did not assign permissions directly to the User to avoid management difficulties later. Instead, I selected **Create group**, named it `Admins`, attached the supreme AWS-managed administrative policy (**`AdministratorAccess`**) to this group, and then added the User `Admin-Cuong` to the group.
4. After initialization, log out of the Root account. Proceed to set up the multi-layered security mechanism **Virtual MFA (Multi-Factor Authentication)** via the Google Authenticator app on a personal mobile device for both the Root account and the IAM account `Admin-Cuong`. From this point forward, all system configuration operations are performed safely on this new IAM User.

##### **4. Screenshots Verification**
<img src="/images/week2/iam-create-user-step1.png" alt="IAM Create User" style="max-width:100%; height:auto;" /> : Detailed screenshot of the IAM User `Admin-Cuong` initialization step, configuring login parameters through the AWS Management Console.
<img src="/images/week2/iam-dashboard.png" alt="IAM Dashboard" style="max-width:100%; height:auto;" /> : Screenshot of the overall IAM Dashboard interface. The screen displays an absolute security compliance status with green checkmarks indicating that the Root account has MFA enabled and the IAM account is protected by a multi-layered structure.

---

#### **LAB 3: Virtual Private Cloud (VPC) - Planning and Designing an Isolated Virtual Network**

##### **1. Overview**
Computer networking is the foundation of every infrastructure system. This Lab provides detailed instructions on the process of personally designing, calculating IP ranges, and building an isolated virtual network called **Amazon VPC (Virtual Private Cloud)** in the cloud, acting as a virtual Data Center to protect the application servers inside.

##### **2. Core Concepts**
* **Calculating the CIDR Block Range:** When designing a VPC, choosing the IP range is extremely critical to avoid overlapping with the internal network (On-premises) when connecting via VPN later. I selected the standard IP range `10.0.0.0/16`. Using the mathematical formula for subnetting, this range provides a total of $2^{(32-16)} = 2^{16} = 65,536$ valid internal IP addresses.
* **Public Subnet & Internet Gateway (IGW):** A Subnet is considered "Public" if and only if it has a clearly defined route in the Route Table pointing out to an Internet Gateway. The IGW acts as an edge router, performing Network Address Translation (NAT) from the internal private IP of the server to a Public IP to communicate with the outside world.

##### **3. Step-by-step Execution**
1. Access the **VPC** control panel. Click the **Create VPC** button, select the manual configuration mode (*VPC only*), name the network `MyLabVPC`, and enter the CIDR range `10.0.0.0/16`.
2. Navigate to **Subnets** > Select **Create subnet**. Select the VPC just created, name this sub-network partition `Public-Subnet-1A`, select the Availability Zone as `us-east-1a`, and assign a narrower sub-CIDR range `10.0.1.0/24` (Providing 256 IP addresses, in which AWS reserves 5 head and tail IPs for system purposes).
3. Navigate to **Internet Gateways** > Click **Create internet gateway**, name it `MyLab-IGW`. After creation, click the **Actions** button > Select **Attach to VPC** and point this gateway directly to `MyLabVPC`.
4. Navigate to **Route Tables**. The system automatically creates a default route table (Main Route Table)

##### **4. Screenshots Verification**
<img src="/images/week2/vpc-architecture.png" alt="VPC Architecture Topology" style="max-width:100%; height:auto;" /> : Logic diagram representing network partition planning, the subdivided structure of CIDR IP ranges, and the packet path through the Internet Gateway.
<img src="/images/week2/vpc-create-success.png" alt="VPC Configuration Success" style="max-width:100%; height:auto;" /> : Summary table of the status on the AWS Console confirming that the network system `MyLabVPC` has transitioned to a clean active state, attached with the exact route table containing the rule line `0.0.0.0/0 -> igw`.

---

#### **LAB 4: Amazon Elastic Compute Cloud (EC2) - Deploying an Automated Virtual Web Server**

##### **1. Overview**
With the security framework and network architecture established, this Lab leverages core compute resources by launching a virtual server using the **Amazon EC2 (Elastic Compute Cloud)** service. To optimize the practical deployment process, I applied a script automation technique (User Data) to transform a raw server instance into a fully functional Apache Web Server without requiring manual SSH command intervention after boot.

##### **2. Core Concepts**
* **Next-Generation Operating System (Amazon Linux 2023 - AL2023):** This is the standard Linux operating system deeply optimized by AWS, removing redundant packages to accelerate boot times, enhance security, and integrate the next-generation package manager `dnf` as a replacement for the legacy `yum`.
* **Stateful Security Group Firewall Mechanism:** A Security Group acts as a virtual firewall controlling traffic at the network layer for each individual virtual server instance. Due to its **Stateful** nature, if an Inbound rule is opened (e.g., port 80 for web users), the Outbound flow (the reverse data response from the server) is automatically allowed without requiring any explicit outbound rules.
* **The Power of User Data Automation:** AWS allows a shell script to be pasted and executed with supreme `root` privileges at the exact moment the server boots for the first time. This standardizes the environment setup process, making software installation uniform and consistent across multiple instances.

##### **3. Step-by-step Execution**
1. From the **EC2** dashboard interface, click the orange **Launch instance** button. In the *Name* field, enter the identifier `MyWebServer` for this virtual server.
2. Under the *Application and OS Images (AMI)* section, select the **Amazon Linux 2023 AMI** 64-bit optimized standard edition.
3. In the *Instance type* section, select the **`t2.micro`** hardware configuration (Providing a single-core 1 vCPU and 1 GiB RAM) to ensure the server runs completely within the Free Tier limits of the AWS ecosystem.
4. In the *Key pair (login)* section, click to create a new secure key pair named `my-key`. The system will automatically download a file named `my-key.pem` to the local machine. This file contains the private key used for encryption and decryption when performing secure SSH administrative connections later.
5. In the *Network settings* section, click the **Edit** button. Modify the default selections to point the server to the custom virtual network **`MyLabVPC`** and the **`Public-Subnet-1A`** partition designed in Lab 3. For the *Auto-assign public IP* field, select **Enable** to allow AWS to allocate a unique public IP address to the server when it goes live.
6. Right below the network section, create a new Security Group named `Web-SG`. Configure two standard secure Inbound rules:
   * Rule 1: Type `SSH`, default port `22`, source set to `My IP` (Restricting administrative terminal access exclusively to my personal machine).
   * Rule 2: Type `HTTP`, standard network port `80`, source set to Any IPv4 (`0.0.0.0/0`) to allow all global internet users to access the website.
7. Scroll to the bottom of the page and expand the **Advanced details** section. Scroll down to the final text box labeled **User data**, then paste the exact automation shell script for environment provisioning below:
   ```bash
   #!/bin/bash
   # Perform a full update on the core operating system libraries
   sudo dnf update -y
   # Download and install the Apache Web Server package (httpd)
   sudo dnf install httpd -y
   # Activate the Apache daemon process immediately
   sudo systemctl start httpd
   # Configure Apache to automatically start on system boot when reloaded
   sudo systemctl enable httpd
   # Overwrite the default index HTML file to verify the application result
   echo "<h1>Welcome to My AWS Web Server running on Docker infrastructure context!</h1>" > /var/www/html/index.html
8. Click the orange **Launch instance** button at the bottom right of the screen to command the AWS infrastructure to provision the actual server instance.

##### **4. Screenshots Verification**
<img src="/images/week2/anh1.png" alt="EC2 Instance Naming" style="max-width:100%; height:auto;" /> : Screenshot of the server naming step `MyWebServer` and the selection of the Amazon Linux 2023 AMI from the repository.
<img src="/images/week2/anh2.png" alt="EC2 Hardware and Key Pair" style="max-width:100%; height:auto;" /> : Evidence of the restricted `t2.micro` hardware configuration and the successful initialization step for the secure private key pair `my-key.pem`.
<img src="/images/week2/anh3.png" alt="EC2 Network Security Groups" style="max-width:100%; height:auto;" /> : Screenshot of the entire Network Settings panel, recording the assignment of the server to the custom network range `MyLabVPC`, allocation of the Public IP, and the firewall configuration opening public port 80.
<img src="/images/week2/anh4.png" alt="EC2 User Data Provisioning" style="max-width:100%; height:auto;" /> : Detailed screenshot of the advanced User Data configuration field, displaying the intact shell script for automatic Apache web service provisioning.
<img src="/images/week2/anh5.png" alt="EC2 Green Running State" style="max-width:100%; height:auto;" /> : Interface of the active instance list, displaying the `MyWebServer` instance line turned into a bright green `Running` state and passing the 2/2 health checks from the AWS infrastructure.
<img src="/images/week2/anh6.png" alt="EC2 Apache Web Server Browser" style="max-width:100%; height:auto;" /> : Actual screenshot of the Chrome browser on the local machine. Upon entering the Public IP address of the server into the URL bar, the webpage immediately displays the large heading line *"Welcome to My AWS Web Server..."*, proving that the automation script worked flawlessly at 100%.

---

#### **LAB 5: Amazon Simple Storage Service (S3) - Source Code Distribution via Static Website Hosting**

##### **1. Overview**
As the volume of files (images, frontend interface source code HTML/CSS/JS) increases, storing them directly on the local disk of an EC2 server wastes compute resources and hinders scalability. This Lab demonstrates how to leverage the market-leading object storage service – **Amazon S3 (Simple Storage Service)**, and configure its Static Website Hosting feature to transform a pure data bucket into a high-performance static website distribution endpoint, capable of handling millions of concurrent users at nearly zero cost.

##### **2. Core Concepts**
* **Object Storage Architecture:** S3 does not manage data in a hierarchical folder tree structure like a traditional hard drive; instead, it manages data in a flat structure as Objects. Each object consists of: Raw data (the actual file), Metadata identifiers (descriptive attributes such as file type and creation date), and a unique Key string acting as the unique resource path.
* **Global Uniqueness of S3 Bucket Names:** When creating a bucket on S3, the name you choose must be absolutely unique across the entire global AWS system, not just within your own account. This is because AWS maps that exact bucket name directly into a public internet domain URL.
* **Advanced Bucket Policy Authorization:** By default upon creation, all data inside S3 is in an absolute secure (Private) state. To transform it into a widely distributed static website, we must write a JSON policy document. This document utilizes the wildcard character `*` in the `Principal` field to denote: Allowing all internet users to execute the file-reading action (`s3:GetObject`).

##### **3. Step-by-step Execution**
1. In the top search bar of the AWS Console, type **S3** and select the service. On the dashboard interface, click the orange **Create bucket** button.
2. In the *Bucket name* field, enter a globally unique identifier (e.g., `cuong-static-website-2026`). In the *Region* section, keep the default `us-east-1` to maintain network infrastructure consistency.
3. Scroll down to the security configuration section labeled *Block Public Access settings for this bucket*. Proceed to uncheck the supreme checkbox **"Block all public access"**. This action is equivalent to unlocking a protective latch, accepting that this bucket has the potential to expose data publicly to the internet if authorized. Check the acknowledgement box below to agree to these settings. Scroll to the bottom of the page and click **Create bucket**.
4. Click directly on the newly created bucket name `cuong-static-website-2026` from the list. Navigate to the **Properties** tab. Scroll down to the very bottom of the page to find the **Static website hosting** section > Click **Edit**.
5. Change the status from *Disable* to **Enable**. Under the *Hosting type* section, select the *Host a static website* option. In the *Index document* index field, enter the exact file name of the structured home page, which is `index.html`. Click to save the configuration. At this point, AWS will automatically generate a link address string called the *Bucket website endpoint* at the bottom of the page.
6. Switch to the tab named **Permissions**. Locate the **Bucket policy** section > Click **Edit**. Proceed to paste the exact following public read access authorization JSON structure into the editor:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadGetObject",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::cuong-static-website-2026/*"
           }
       ]
   }
*(Technical Note: The `/*` character at the end of the Resource string denotes applying read permissions to all files inside this bucket).* Click to save the policy.
7. Return to the first tab, **Objects**. Click the **Upload** button > Select **Add files** and choose an existing user interface file `index.html` from your local machine to upload to the system.

##### **4. Screenshots Verification**
<img src="/images/week2/anh7.png" alt="S3 Bucket Creation" style="max-width:100%; height:auto;" /> : Interface of the successfully initialized S3 Bucket, recording the unique identifier configuration and the successful removal of the default block public access shield.
<img src="/images/week2/anh8.png" alt="S3 Properties Static Website Hosting" style="max-width:100%; height:auto;" /> : Screenshot of the Properties section confirming that the Static website hosting feature has been toggled to an active green state along with the declaration of the default index file `index.html`.
<img src="/images/week2/anh9.png" alt="S3 Bucket Policy Editor" style="max-width:100%; height:auto;" /> : Screenshot of the Bucket Policy editor interface, displaying the intact JSON authorization code for wide-scale file read access without generating any syntax errors.
<img src="/images/week2/anh10.png" alt="S3 Object Upload Success" style="max-width:100%; height:auto;" /> : Object management list table displaying the successful upload status of the source code file `index.html` to the cloud, showing a green *Succeeded* state.
<img src="/images/week2/anh11.png" alt="S3 Global Endpoint Browser Verification" style="max-width:100%; height:auto;" /> : Actual screenshot of the finalized website running smoothly in the browser when users click directly on the URL Endpoint link distributed globally by the S3 service.

---

#### **LAB 6: Amazon Relational Database Service (RDS) - Provisioning a Managed Relational Database Infrastructure**

##### **1. Overview**
The final puzzle piece required to complete a full application architecture is structured data storage. This Lab provides detailed instructions on the process of personally deploying the world's most popular open-source relational database engine – **MySQL Server** – using the automated managed service **Amazon RDS (Relational Database Service)**. The core objective of this lab is to handle interface conflicts to minimize hardware configurations, ensuring the account runs safely within the Free Tier limits.

##### **2. Core Concepts**
* **The Advantages of a Managed Database Service (RDS):** If we manually install MySQL on an EC2 instance, we have to handle everything from operating system patching and backup configurations to setting up replication clusters. By utilizing Amazon RDS, all of those heavy infrastructure administration tasks are fully automated by AWS, allowing developers to focus 100% on optimizing SQL queries.
* **Endpoint Mechanism and Connection Topology:** Once a database is initialized on RDS, the system does not provision a static IP address for direct connection. Instead, AWS provides a unique DNS string called an **Endpoint**. When configuring backend applications (such as Spring Boot, Next.js, or NestJS), developers point this Endpoint string inside the environment variable files to execute secure data query sessions via the default network port `3306`.

##### **3. Step-by-step Execution**
1. In the main search bar of the AWS Console, type `RDS`. From the resulting list, select the **Aurora and RDS** service (Featuring a blue cube icon).
2. On the main control panel, click the orange **Create database** button. Proceed to configure the details according to the following standardized technical parameters:
   * *Choose a database creation method*: Select the **Standard create** option to display full granular control over hardware parameters from scratch.
   * *Engine options*: Select the dolphin icon representing the **MySQL** database management system.
   * *Templates*: Scroll down. Since the latest AWS user interface update has modified the terminology, select the **Dev/Test** template option here (or an equivalent Sandbox configuration package) so that the system allows lowering the server configuration to maximum savings.
3. Under the identity account configuration section labeled **Settings**:
   * *DB instance identifier*: Name the administrative database instance `my-docker-db`.
   * *Master username*: Keep the default system identifier `admin`.
   * *Credentials management*: Select the *Self managed* option. In the *Master password* and *Confirm master password* text boxes, enter the exact string: **`DockerDB.2026`**. *(Core Technical Note: Absolutely do not include the special character `@` due to the AWS RDS parser rules, which treat this as a syntax error character and lock the configuration selection menu below).*
4. Under the resource configuration section labeled **Instance configuration**:
   * In the *Instance type* dropdown menu, select the smallest resource-saving virtual instance line, **`db.t3.micro`** (Providing a dual-core 2 vCPUs and 1 GiB RAM configuration), which is a chip line completely under the protection of the AWS Free Tier catalog.
5. Under the disk capacity configuration section labeled **Storage**:
   * *Storage type*: Select the next-generation, performance-optimized storage technology, **General Purpose SSD (gp3)**.
   * *Allocated storage*: Completely clear the large default system number and enter the exact low data number: **`20` GiB** (The standard storage allocation granted by AWS for free for educational purposes).
6. Scroll directly to the bottom of the page, keep all other secure default parameters intact, and click the large orange **Create database** button. The system will redirect back to the main RDS Databases management list.

##### **4. Screenshots Verification**
<img src="/images/week2/anh12.png" alt="RDS MySQL Engine Selection" style="max-width:100%; height:auto;" /> : Screenshot of the MySQL Engine selection step combined with selecting the Dev/Test source code template partition on the RDS Database creation interface.
<img src="/images/week2/anh13.png" alt="RDS Instance Size and Storage gp3" style="max-width:100%; height:auto;" /> : Evidence recording the successful declaration of a secure standard password containing no forbidden characters, and the step lowering the chip configuration to the `db.t3.micro` line with a gp3 disk partition limited to 20 GiB of data.
<img src="/images/week2/anh14.png" alt="RDS Database Available State and Endpoint" style="max-width:100%; height:auto;" /> : Screenshot of the finalized Databases management list. The database row name `my-docker-db` has transitioned from initialization to a fully stable, active green state showing **`Available`**, while displaying the complete Endpoint connection string ready for future backend connections.

---

### V. Infrastructure Challenges, Error Resolution Logs & Expert Perspectives

Throughout the execution of this week's complex series of 6 infrastructure Labs, I constantly faced real-world problems and extracted brutal lessons learned:

* **The "Hidden Cost" Problem of Automatic NAT Gateways:** When planning the network architecture topology in Lab 3 (VPC), the AWS automated configuration wizard continuously recommended initializing the system with 1 attached NAT Gateway to serve the Private network. By deeply analyzing the infrastructure cost breakdown, I realized that NAT Gateways are billed based on actual uptime hours at a very expensive rate ($0.045/hour), exceeding the scope of an educational account. I proactively selected "None" for this network configuration option, routing the entire connection flow directly through the edge Internet Gateway to completely resolve the learning objective without generating a massive bill on the Sandbox account.
* **The Interface Conflict Bug Locking the Hardware Menu (RDS UI Bug Loop):** The biggest challenge of the week occurred in Lab 6, where the new AWS RDS creation interface continuously froze and grayed out (Disabled) the entire server chip selection menu, throwing a red stuck loop error in the storage section. Through digging deep into the root cause, I discovered this is a notorious UI Bug on the new dashboard when accounts utilize strong passwords containing the `@` character (e.g., `DockerDB@2026`). The AWS RDS parser misinterprets the `@` character as part of an internal domain resolution routing string, thereby locking all subsequent processes. By sanitizing the password to use a dot delimiter like `DockerDB.2026` and proactively forcing the gp3 storage type selection first, the system immediately unlocked the `db.t3.micro` server line.
* **In-Depth Analysis of Network Layer Security Mechanisms (Stateless vs. Stateful):** I spent significant time dissecting the operational nature of the two security shields on AWS virtual networks: Security Groups and Network ACLs (NACLs). Security Groups operate at the virtual server instance level and are **Stateful**, simplifying the configuration workflow because you only need to focus on opening the inbound ports. Conversely, Network ACLs operate at the boundary covering the entire Subnet partition and are completely **Stateless** – meaning that if an inbound port is opened (Inbound), you must manually write an additional rule to open the exact ephemeral ports range (Ephemeral Ports 1024-65535) on the outbound response flow (Outbound) for traffic to flow; otherwise, the system will block it entirely.

---

### VI. Professional Reflections

Personally configuring everything successfully and watching a data packet travel in a sequential manner—originating from the public internet outside, passing through the edge Internet Gateway router, being precisely guided by the routing rules within the Route Table to hit the exact EC2 virtual server instance deep inside the Subnet partition, and from there initiating secure database connection query sessions to the RDS Database instance—is the most valuable technology experience I have accumulated to date.

Cloud Engineering is absolutely not a set of random, lucky clicks based on intuitive graphical user interfaces. It is a scientific discipline that demands clear logical thinking, mathematically precise address space calculations, and intentional infrastructure design grounded in optimization framework rules and standards (*AWS Well-Architected Framework*). Mastering this core infrastructure serves as a rock-solid launching pad for me to dive deeper into automated containerized application packaging solutions in the upcoming phases of my internship.

---

### VII. Strategic Plan & Optimization Roadmap for the Upcoming Week

To pave the way for the next advanced phases of the project and further optimize system architecture capabilities, next week's action plan will focus on deploying the following core pillars:

* **Expanding Advanced Lab Series:** Continue designing and executing subsequent in-depth Labs within the AWS Sandbox environment to master Auto Scaling mechanisms, Elastic Load Balancing (ELB), and system monitoring via Amazon CloudWatch.
* **Researching Real-World Application Modules:** Deeply leverage high-quality educational resources on YouTube to analyze code structures, tiered architecture diagrams, and methods for integrating complex functional modules into cloud environments.
* **Accumulating In-Depth Expertise:** Dedicate structural time to studying technical lectures and tutorial series from industry Solutions Architects on YouTube to update modern design mindsets, troubleshoot performance bottlenecks, and fully prepare for containerized application packaging.