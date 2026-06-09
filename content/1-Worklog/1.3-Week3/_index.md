---
title: "Week 3: Advanced Network Architecture Expansion, Hybrid DNS and Enterprise AWS CLI Administration"
date: 2026-05-05
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---


### I. Executive Summary
This week marks a strategic shift in my internship roadmap during the First Cloud AI Journey – Workforce Bootcamp 2026 at the AWS Vietnam Office. I transitioned from single-tier infrastructure design to building complex multi-tier enterprise networks and hybrid connectivity across 6 major Labs: Lab 7 (Internal Subnet Architecture), Lab 8 (VPC Routing & Ingress Gateways), Lab 10 (Route 53 Hybrid DNS Resolver), Lab 11 (Administration via AWS CLI), Lab 13 (Isolated Multi-Tier Advanced VPC Topology), and Lab 14 (Elastic Load Balancing for traffic distribution).

### II. Strategic Objectives of the Week
* **Isolated Network Stratification (Advanced VPC Engineering):** Design in-depth multi-layer network topologies, segmenting subnets to completely isolate the database and backend layers from the public Web tier.
* **Hybrid Cloud Network Integration (Hybrid Cloud DNS):** Realize bidirectional domain name resolution between Cloud and On-Premises via Route 53 Resolver, safeguarding the internal naming architecture.
* **Scripted Infrastructure Automation (CLI Automation):** Master the AWS CLI command line interface combined with JSON JMESPath query filters to extract large-scale infrastructure data without depending on the Web Management Console.
* **Highly Available Traffic Distribution (High Availability):** Deploy Elastic Load Balancing to automate data flow redirection, eliminating Single Points of Failure (SPOF) for the application hosting stack.

---

### III. Activity Log & Detailed Roadmap (From 05/05/2026 to 11/05/2026)

| Timeframe | Activity Category | In-depth Operational Tasks Executed | Results / Deliverables Achieved |
| :--- | :--- | :--- | :--- |
| **Day 1** *(05/05)* | Subnet Architecture | Initialize custom VPC and plan public and private redundant Multi-AZ Subnets partitions. (Lab 7) | Foundation network infrastructure ready; secure logical boundaries established. |
| **Day 2** *(06/05)* | Ingress Routing | Initialize Internet Gateway (IGW), attach to VPC, and customize public Route Tables routing outwards. (Lab 8) | Two-way internet communication successfully enabled for Edge network partitions. |
| **Day 3-4** *(07-08/05)* | Hybrid DNS Connection | Initialize Private Hosted Zone, configure Route 53 Resolver Inbound/Outbound Endpoints across Multi-AZ, and conduct FinOps resource cleanup. (Lab 10) | Two-way internal domain resolution successfully enabled between cloud and corporate data centers. |
| **Day 4** *(08/05)* | CLI Administration | Bypass CloudShell limitations, configure local terminal authentication, and execute data extraction queries for EC2 using JMESPath table formatting. (Lab 11) | Resource control managed via command line, eliminating bulky raw JSON outputs. |
| **Day 5** *(09/05)* | Multi-Tier Advanced Network | Deploy the Advanced VPC Topology model, distributing multi-tier subnets to strictly isolate sensitive DB tiers from Web Servers. (Lab 13) | Network security boundaries solidly established through multiple layers of defense. |
| **Day 6** *(10/05)* | Load Balancing | Initialize an Elastic Load Balancer (ELB) to intelligently route traffic to foundational Web Instances. (Lab 14) | System achieves High Availability, eliminating the risk of localized node failures. |
| **Day 7** *(11/05)* | Report Packaging | Compile technical documentation, migrate image sources into static HTML elements, and package the Portfolio on the Hugo platform. | Week 3 activity log running clean and live on GitHub Pages. |

---

### IV. Technical Deep Dives & Detailed Analysis of the 6 Labs

#### **1. Lab 7: Amazon CloudWatch & AWS Budgets - Setting Up Corporate Budgets and Proactive Monitoring Alarms**

##### **Overview**
The core requirement of any enterprise-grade cloud deployment is strictly controlling operational costs and setting up proactive resource monitoring systems. In this Lab, I constructed a foundational **AWS Budgets** structure to manage financial boundaries and utilized **Amazon CloudWatch** to track system performance in real-time, preventing the risk of out-of-control cost escalations.

##### **Core Concepts**
* **AWS Budgets:** A FinOps governance tool that enables the creation of custom cost limits, tracks Monthly Recurring renewal cycles, and automatically calculates financial consumption forecast scenarios.
* **CloudWatch Metrics & Alarms:** An operational metric collection system (such as `CPUUtilization`). When resources exceed configured thresholds, the system immediately triggers an alert state (`ALARM`) and dispatches notifications via Amazon SNS.

##### **Step-by-step Execution**

###### **Step 1: Configuring cost limits and financial routing filters**
I proceeded to initialize a fixed monthly budget policy with a limit of `20.00 USD`. The system was configured with advanced filters focusing on the cost dimensions of EC2 virtual server instances to strictly monitor experimental workloads.
<img src="/images/week3/1.png" alt="Configuring AWS Budgets cost limits" style="max-width:100%; height:auto;" />

###### **Step 2: Establishing multi-tier financial alert thresholds**
To ensure absolute safety, I configured 3 alarm tiers based on consumption percentages: Alarm Tier 1 triggers when Forecasted costs hit 80%, Tier 2 triggers at 100% of Forecasted costs, and Tier 3 activates immediately when Actual expenses exceed 100% of the allocated budget.
<img src="/images/week3/2.png" alt="Reviewing multi-tier financial alert structures" style="max-width:100%; height:auto;" />

###### **Step 3: Validating the operational status of the budget management system**
The budget policy named `My AWS budget` was successfully created on the dashboard. The status display showing clean green (`OK` and `Healthy`) confirms that the FinOps system has officially started tracking cloud account cash flows.
<img src="/images/week3/3.png" alt="Validating successful budget activation status" style="max-width:100%; height:auto;" />

###### **Step 4: Building an infrastructure dashboard for real-time CPU performance**
Switching to the infrastructure monitoring component, I initialized a custom dashboard named `EC2-Monitor-Dashboard` on Amazon CloudWatch, configuring graph widgets to continuously aggregate processor consumption metrics (`CPUUtilization`).
<img src="/images/week3/4.png" alt="Dashboard tracking CPUUtilization metrics on CloudWatch" style="max-width:100%; height:auto;" />

###### **Step 5: Configuring the processor overload Alarm system**
I configured an automated alarm named `EC2-High-CPU-Alarm`. The triggering condition was precisely programmed: if the `CPUUtilization > 80%` metric persists consecutively within 1 data datapoint (5 minutes), the system will immediately pivot to an alert state for rapid engineering intervention.
<img src="/images/week3/5.png" alt="Setting up automated CloudWatch Alarm triggers" style="max-width:100%; height:auto;" />

---

#### **2. Lab 8: Amazon Route 53 - Planning and Initializing Internal Private Hosted Zone Systems**

##### **Overview**
An isolated network topology cannot communicate securely if server components must call each other directly via volatile raw IP addresses. This Lab focuses on establishing an **Amazon Route 53 Private Hosted Zone**, building a secure internal domain name space completely walled off from the public internet.

##### **Core Concepts**
* **Private Hosted Zone (PHZ):** A container block holding internal DNS records completely hidden from the external internet. Domain resolution queries are only valid within the boundaries of designated and associated VPC virtual networks.
* **DNS Resolution & DNS Hostnames:** Mandatory configuration attributes that must be enabled at the VPC level to permit virtual server instances to send recursive queries to the default `AWS-provided DNS server`.

##### **Step-by-step Execution**
I proceeded to create a Private Hosted Zone under the internal enterprise domain name `hutech.local`. In the configuration interface, the custom virtual network `VPC ID` was selected to map directly with this Hosted Zone, ensuring all server resources located inside the internal network block have the ability to resolve domain names securely.
<img src="/images/week3/6.png" alt="Initializing internal domain Private Hosted Zone configurations" style="max-width:100%; height:auto;" />

---

#### **3. Lab 10: Amazon Route 53 Resolver - Integrating Hybrid DNS Connectivity Architecture**

##### **Overview**
In Hybrid Cloud architectures, corporate or university internal networks need to seamlessly resolve internal AWS domains, and conversely, cloud-hosted servers must be able to read local data center resources. This Lab realizes that native networking bridge by deploying **Amazon Route 53 Resolver Endpoints**.

##### **Core Concepts**
* **Inbound Endpoint:** A redundant pair of Elastic Network Interfaces (ENIs) possessing dedicated private IPs within the VPC, acting as the primary ingestion points to listen to and accept DNS queries forwarded from the On-Premises environment into internal AWS zones.
* **Outbound Endpoint:** The infrastructure component that intercepts DNS queries originating from the cloud stack and forwards them securely to external local DNS Servers based on Conditional Forwarding Rules.

##### **Step-by-step Execution**

###### **Step 1: Designing the configuration for the Inbound Endpoint**
I initialized the configuration for the inbound ingestion entry point named `Hutech-Inbound-Endpoint`. To guarantee high fault tolerance and eliminate Single Points of Failure (SPOF), the system strictly mandates network interface distribution across a minimum of two separate Availability Zones (`us-east-1a` and `us-east-1b`) bound to automatic IP allocations.
<img src="/images/week3/7.png" alt="Configuring Multi-AZ allocation for Inbound Endpoint" style="max-width:100%; height:auto;" />

###### **Step 2: Initializing the Outbound Endpoint component and auditing operational health**
To establish the bidirectional resolution flow, I deployed the outbound egress component `Hutech-Outbound-Endpoint` utilizing the same high-availability Multi-AZ distribution model. The monitoring subsystem recorded the operational status shifting to a steady green (`Operational`), confirming that the ENIs are ready to route packets in real-time.
<img src="/images/week3/8.png" alt="Validating Operational status of the Outbound Endpoint" style="max-width:100%; height:auto;" />

---

#### **4. Lab 11: Enterprise Cloud Infrastructure Governance via AWS CLI Command Line**

##### **Overview**
The **AWS Command Line Interface (AWS CLI)** shifts the entire system management paradigm from manual, error-prone clicks on a graphical user interface into automated, precise, and scriptable command structures. This empowers engineers to automate infrastructure tasks and programmatically extract system statuses.

##### **Core Concepts**
* **AWS CloudShell:** An integrated browser-based management terminal that automatically authenticates account session details and pre-packs the complete AWS CLI development toolkit to optimize maintenance timelines.
* **JMESPath Query Filter (`--query`):** A client-side query language designed for JSON data structures, helping to select, trim, and strip away redundant fields, keeping only the core operational attributes.

##### **Step-by-step Execution**

###### **Step 1: Launching a secure authenticated command line environment**
I activated the online administrative terminal environment via AWS CloudShell. The system automatically provisioned a secure, authorized working session mapped directly to the active IAM User's permission scope.

###### **Step 2: Constructing and executing advanced filtered data queries**
Instead of invoking a standard EC2 description command which spits out dozens of pages of raw, bulky JSON payload data, I constructed a precise JMESPath query filter to harvest exactly 3 vital operational attributes: Instance ID, Lifecycle State, and Hardware Configuration Type, outputting into a crisp ASCII table layout.
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name,InstanceType]" --output table
```
---

###### **Step 3: Analyzing and validating structured infrastructure tabular output**
The API gateway processed the authenticated request and returned a structured text matrix, completely eliminating bulky raw JSON data. The terminal output displayed the active lab machine with its Instance ID (`i-058d40dc31f87c225`), lifecycle running state (`running`), and hardware classification (`t2.micro`), confirming the cloud infrastructure is executing correctly under direct command line control.
<img src="/images/week3/9.png" alt="Validating CLI tabular command execution output" style="max-width:100%; height:auto;" />

---

#### **5. Lab 13: Advanced VPC Topology - Multi-Tier Network Isolation Architecture and Subnet Routing Configuration**

##### **1. Overview**
As enterprise infrastructure scales up, a flat or single-layer network model (Flat Network) is no longer sufficient to shield sensitive backend components from cyber security threats. This Lab implements an advanced network routing topology (Advanced VPC Topology), deploying a Multi-tier Subnet layout to distinctly segment the public internet interface layer, the internal application business logic layer, and the core database storage layer. Setting up this isolated subnet ecosystem guarantees intentional data flow traffic management and deep security enforcement.

##### **2. Core Technical Concepts**
* **3-Tier Architecture:** A standardized network blueprint that logically divides the ecosystem into 3 isolated layers: The public tier (Public/Web Tier) accepting inbound internet traffic; the application tier (Application Tier) executing core business logic; and the database tier (Database Tier) completely isolated to house sensitive state assets.
* **Isolation Control & Route Tables Structure:** The enforcement mechanism of packet flows at the routing layer. By implementing separate route tables for each subnet layer, we completely block public internet entities from scanning, sniffing, or directly reaching the internal Database boundaries.
* **CIDR (Classless Inter-Domain Routing) IP Allocation Planning:** Scientifically mapping out IP subnet networks to eliminate block overlaps, optimize address space efficiency, and establish pre-conditions for precise firewall definitions (Security Groups / NACLs) later.

##### **3. Step-by-step Execution**

###### **Step 1: Initializing and allocating dedicated infrastructure subnet ranges**
To expand the existing network topology of `MyLabVPC`, I proceeded to initialize new isolated subnet networks exclusively serving the internal data storage layer. This segment was named `Private-DB-Subnet-1A`, assigned to the designated Availability Zone, and mapped out to a tight, highly isolated CIDR network space of `10.0.3.0/24`. The registration process on the AWS Management Console completed successfully, and the system logged an active status.
<img src="/images/week3/10.png" alt="Declaring isolated Subnet parameters for Database" style="max-width:100%; height:auto;" />

The newly configured subnet layout was synchronized and visualized on the `MyLabVPC` interactive architecture map topology, ensuring that management attributes regarding VPC ID, logical attachment state, and original network routing paths were accurately established.
<img src="/images/week3/11.png" alt="Validating new Subnet status inside the VPC Dashboard" style="max-width:100%; height:auto;" />

###### **Step 2: Generating independent Route Tables and configuring Edge data isolation rules**
An isolated subnet is only truly secure when guided by an independent routing entity. I configured a brand new route table designated as `DB-Route-Table` within `MyLabVPC`. This route table was designed with strict intent: absolutely no default outbound destination rule (`0.0.0.0/0 -> igw`) was added, effectively cutting off all direct external traffic paths from entering this subnet boundary.
<img src="/images/week3/12.png" alt="Initializing the isolated DB-Route-Table entity" style="max-width:100%; height:auto;" />

Following the route table initialization, I executed the Subnet Association phase, mapping the `Private-DB-Subnet-1A` network directly to the newly crafted `DB-Route-Table`. This configuration officially detaches the storage block from the influence of the public Internet Gateway border, locking down fortified multi-tier security perimeters for the cloud environment.
<img src="/images/week3/13.png" alt="Mapping the Database Subnet association to the isolated route table" style="max-width:100%; height:auto;" />

---

#### **6. Lab 14: Elastic Load Balancing - Deploying Traffic Distribution Infrastructure and Highly Available Load Balancers**

##### **1. Overview**
In production environments, an application (such as a tour booking system or a job recruitment portal) running on a single standalone virtual server faces massive service crash risks during traffic spikes or hardware failure events (Single Point of Failure). This Lab permanently resolves the traffic load handling problem and guarantees **High Availability** by deploying an intelligent Layer 7 **Amazon ELB (Elastic Load Balancing)** solution. The load balancer acts as the singular public entry point for all outbound traffic and automatically distributes data streams across destination computing backends optimally.

##### **2. Core Technical Concepts**
* **Application Load Balancer (ALB):** A traffic routing engine operating at Layer 7 of the OSI model. ALB possesses the capability to inspect deep into HTTP/HTTPS payloads, evaluating attributes like URL paths or HTTP headers to route traffic intelligently to different downstream target pools.
* **Target Group & Target Registration:** A logical resource grouping containing the array of compute EC2 servers responsible for processing incoming requests. The ALB relies on this registry map to distribute user traffic based on load balancing algorithms (such as Round Robin).
* **Proactive Health Checks:** An automated mechanism where the ALB continuously transmits periodic health probes (pings) to registered servers within the Target Group over a configured protocol and path. If a machine fails to respond (Unhealthy), the ALB instantly isolates that node, halts packet delivery to it, and reroutes traffic streams to the remaining healthy instances, maintaining zero application downtime.

##### **3. Step-by-step Execution**

###### **Step 1: Launching the Application Load Balancer instance configuration**
From the Amazon EC2 management module, I navigated to the Load Balancing tab and initiated an Application Load Balancer setup. The entity was assigned the identifier name `MyWebALB`, configured with an Internet-facing scheme to serve as the public traffic entry gate, and set to resolve standard IPv4 addresses.
<img src="/images/week3/14.png" alt="Setting basic parameters for the Application Load Balancer" style="max-width:100%; height:auto;" />

To guarantee redundant fault architecture and wide-area High Availability, I executed the ALB Network Mapping configuration. This traffic distribution engine was mapped directly into the `MyLabVPC` network and explicitly assigned to run concurrently across two public subnets spanning distinct Availability Zones (Multi-AZ), guaranteeing that the application architecture survives even if a physical AWS data center encounters a hardware disaster event.
<img src="/images/week3/15.png" alt="Configuring Multi-AZ network mapping redundancy for the load balancer" style="max-width:100%; height:auto;" />

###### **Step 2: Structuring the Target Group and setting up active Health Check mechanisms**
Next, I constructed a Target Group named `Web-TG` operating on the HTTP protocol over web-standard port 80 to act as the destination landing pad for incoming streams passing through the ALB. Within the advanced health monitoring setup, I declared the default health probe path as `/` along with threshold parameters defining response Timeout, check cycles, and maximum consecutive retry thresholds before finalizing a server's health status.

Following that, I registered the existing EC2 compute hosts into this Target Group pool, activating the tracking metrics and rendering them ready to receive distributed request packets from the ALB load balancer.
<img src="/images/week3/16.png" alt="Initializing and configuring the Target Group setup" style="max-width:100%; height:auto;" />

---

### V. Infrastructure Challenges, Troubleshooting Logs & Expert Perspectives

Throughout the execution of this week's complex 6-lab core infrastructure track, I constantly faced real-world architectural issues and extracted invaluable lessons:

* **The "Hidden Cost" Dilemma of Automated NAT Gateways:** During the network topology design phase in Lab 3 (VPC), the automated workflow configuration of AWS constantly recommended initializing the architecture with an attached NAT Gateway to serve the Private subnet. By analyzing the infrastructure cost matrix deeply, I realized that NAT Gateways are charged very expensively by actual running hours ($0.045/hour), which is beyond the scope of a learning account. I proactively selected "None" for this network component, driving the entire connection flow straight through the edge Internet Gateway to perfectly fulfill the lesson objective without generating multi-million VND bills on the Sandbox account.
* **Resolving Operational Bottlenecks:** Cloud operations rarely proceed in a perfectly straight line. When managed cloud services such as AWS CloudShell experience regional restrictions or verification lockouts, a systems engineer must pivot rapidly—whether by migrating execution environments, configuring local terminal proxies, or utilizing alternative shells to sustain deployment momentum.
* **Lifecycle Discipline and Cost Controls:** Automated cloud environments demand strict compliance with resource lifecycle management. Leaving unutilized architectures running—especially heavy network-intensive components like Route 53 Resolver Endpoints or unassociated Elastic IPs—inflicts unnecessary operational costs. Establishing a systematic workflow of resource creation, verification, and tearing down is a foundational habit of an efficient cloud professional.

---

### VI. Professional Reflections

Manually configuring and witnessing a data packet navigate sequentially: starting from the external public internet, crossing the edge Internet Gateway router, being correctly routed by the routing lines inside the Route Table to precisely reach the Application Load Balancer, and from there smoothly distributing across EC2 web server instances sitting deep inside a multi-tier secure network layer is the most valuable engineering experience I have accumulated to date.

Cloud Engineering is absolutely not a series of random, lucky clicks on an intuitive graphical user interface. It is a rigorous science that demands clear logical thinking, mathematically precise address space allocation, and intentional architectural design aligned with optimal frameworks (*AWS Well-Architected Framework*). Mastering this core infrastructure serves as a rock-solid launching pad for me to dive deeper into automated containerized application packaging tracks in the upcoming phases of my internship.

---

### VII. Strategic Planning & Optimization Roadmap for Next Week

To arm myself for the upcoming advanced phases of the project and optimize system architectural capabilities, next week's execution track will focus on launching the following core thrusts:

* **Expanding Advanced Lab Trajectories:** Continue designing and executing practical deployments for the next set of deep-dive Labs on the AWS Sandbox platform to master Auto Scaling Groups (Lab 15) and CDN content distribution networks (Amazon CloudFront - Lab 16).
* **Analyzing Real-World Production Modules:** Delve deep into high-quality educational resources on YouTube to break down structural designs, multi-layered architecture diagrams, and the methodologies for integrating complex functional feature modules into the cloud framework.
* **Accumulating Advanced Subject Expertise:** Dedicate specific blocks of time to study engineering lectures and technical video walkthroughs from Solution Architects on YouTube to update optimal design mindsets, solve performance bottlenecks, and fully prepare for automated application Containerization.