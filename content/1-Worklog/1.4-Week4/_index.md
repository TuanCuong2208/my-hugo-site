---
title: "Week 4: Hybrid DNS Integration and AWS CLI Management"
date: 2026-05-25
weight: 4
chapter: false
pre: "<b>1.4. </b>"
---

During this week, I focused on advanced networking and infrastructure management tasks on AWS. The primary objectives were implementing a hybrid DNS resolution mechanism using Amazon Route 53 Resolver to bridge cloud and local enterprise networks, and optimizing operational workflows through the AWS Command Line Interface (AWS CLI).

---

## 1. Lab 7: Amazon VPC - Internal Subnet Architecture

The core requirement of any enterprise-grade deployment is establishing an isolated virtual network. In this lab, I built the underlying **Amazon VPC (Virtual Private Cloud)** structure to securely host system assets and ensure controlled boundary separation.

### Core Concepts:
* **CIDR Block:** A method for allocating IP addresses and routing Internet Protocol packets without waste (e.g., `10.0.0.0/16`).
* **Subnet Isolation:** Separating frontend resources from sensitive database backends to control logical boundaries at the network level.

### Implementation Process:

#### Step 1: Initialize Virtual Private Cloud (VPC)
I deployed a custom VPC named `MyLabVPC` with a wide `10.0.0.0/16` IP range, creating a completely isolated sandbox environment dedicated to corporate applications.
![Step 1](/images/week4/1.png)

#### Step 2: Provision Public Subnets for Edge Components
I carved out the first subnet segment as a Public Subnet inside the `us-east-1a` Availability Zone. This network interface layer handles connectivity to exterior endpoints and public interfaces.
![Step 2](/images/week4/2.png)

#### Step 3: Map Out Multi-AZ Redundancy Zones
To prevent single-point-of-failure vulnerabilities, I extended the infrastructure by mapping out additional subnets. This strict separation satisfies high-availability criteria for subsequent deployments.
![Step 3](/images/week4/3.png)

---

## 2. Lab 8: VPC Routing and Ingress Gateways

An isolated VPC cannot communicate with external services without explicit routing components. This lab focused on plumbing the structural connections required to direct traffic safely between cloud workloads and exterior endpoints.

### Core Concepts:
* **Internet Gateway (IGW):** A horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
* **Route Tables:** A set of rules, called routes, used to determine where network traffic from subnets or gateways is directed.

### Implementation Process:

#### Step 1: Attach the Internet Gateway (IGW)
I initialized a virtual gateway and bound it directly to `MyLabVPC`, providing a logical bridge for inbound and outbound communication paths.
![Step 4](/images/week4/4.png)

#### Step 2: Update Ingress and Egress Route Mappings
I modified the active public Route Table by appending a default route (`0.0.0.0/0`) targeting the newly deployed Internet Gateway, allowing nodes to process internet-facing requests.
![Step 5](/images/week4/5.png)

---

## 3. Lab 10: Amazon Route 53 - Hybrid DNS Resolver Integration

**Amazon Route 53 Resolver** provides a native bridge for hybrid cloud environments. In enterprise deployment, corporate networks (On-Premises, such as a local university intranet) need to resolve internal AWS cloud domains seamlessly, while AWS workloads simultaneously require resolution for local data center assets without exposing internal topologies to the public internet.

### Core Concepts:
* **Private Hosted Zone (PHZ):** A localized container holding DNS records for a domain that should remain invisible to the public internet, resolvable exclusively within specified, authoritatively associated VPCs.
* **Inbound Endpoint:** A redundant pair of Elastic Network Interfaces (ENIs) with dedicated internal IPs inside the VPC. They serve as target listeners for external or on-premises DNS forwarders routing queries into AWS.
* **Outbound Endpoint:** Network interfaces used to intercept specific cloud-originated DNS queries and securely forward them out to external on-premises DNS servers based on conditional routing rules.
* **Authoritative Split-Horizon Records:** The automated generation of Start of Authority (SOA) and Name Server (NS) records that isolate cloud internal naming structures from public internet recursive loops.

### Implementation Process:

#### Step 1: Create the Private Hosted Zone
I initialized a Private Hosted Zone under the internal domain name `hutech.local`. This zone was explicitly associated with the working VPC. Upon creation, Route 53 instantly provisioned the mandatory SOA metadata and a set of local Name Servers to handle authoritative answers internally.
![Step 6](/images/week4/6.png)

#### Step 2: Configure Route 53 Resolver Inbound Endpoint
To accept incoming recursive requests from external systems, I initialized the setup of an Inbound Endpoint named `Hutech-Inbound-Endpoint`. During the allocation phase, AWS enforces a mandatory architectural constraint: endpoints must span a minimum of two separate Availability Zones (`us-east-1a` and `us-east-1b`) to guarantee fault tolerance and mitigate single-point-of-failure risks.

Due to strict IP availability constraints inside the initial custom lab VPC, the configuration was dynamically migrated to the pre-configured Default VPC. This tactical adjustment provided a clean subnet map across multiple zones, unlocking the interface gray-out state and allowing the assignment of automatically selected internal IPv4 addresses.
![Step 7](/images/week4/7.png)

#### Step 3: Initialize Outbound Endpoints and Monitor Operational Status
To establish complete bidirectional resolution, I configured the complementary Outbound Endpoint named `Hutech-Outbound-Endpoint` utilizing the same high-availability multi-AZ distribution pattern. Both endpoints were tracked until their statuses transitioned to `Operational`, meaning the network interfaces were successfully bound and ready to process real-time packet forwarding.
![Step 8](/images/week4/8.png)

#### Step 4: Execute Resource Deallocation and Cloud Clean-Up
Adhering strictly to the AWS Well-Architected Framework's Cost Optimization pillar, a precise decommissioning sequence was executed once operational testing concluded. Because active Resolver Endpoints incur ongoing hourly charges for underlying ENIs, the resource hierarchy was cleaned up in reverse order: the Outbound and Inbound Endpoints were systematically unlinked and deleted to release reserved IPs, followed by the safe deletion of the `hutech.local` Private Hosted Zone.

---

## 4. Lab 11: Enterprise Cloud Infrastructure Administration via AWS CLI

The **AWS Command Line Interface (AWS CLI)** shifts system management from manual, error-prone graphical clicks to scriptable, automated command executions. This command-line structure allows engineers to manage thousands of resources concurrently, build infrastructure-as-code helper hooks, and extract deterministic state outputs.

### Core Concepts:
* **AWS CloudShell:** A browser-accessible, pre-authenticated administration terminal loaded with the full AWS CLI tool suite, eliminating local credential handling during cloud maintenance windows.
* **JMESPath Query Engine (`--query`):** A client-side JSON query language native to the AWS CLI, used to parse, select, and flatten massive API responses into specific key-value arrays.
* **Output Matrix Restructuring (`--output table`):** A formatting directive that decodes raw JSON payloads into clean, human-readable ASCII tables for instant operational assessment.

### Implementation Process:

#### Step 1: Identify System Constraints and Alternative Execution Vectors
When launching the web-integrated AWS CloudShell in the primary region, the environment encountered a restrictive tenant status lock: `Unable to create the environment. Your account verification is in progress...`. This is a common service-quota throttling mechanism applied to academic or sandboxed lab accounts during heavy utilization. 

To bypass this roadblock without halting operations, the execution vector was offloaded to an alternative authenticated terminal environment, demonstrating flexible problem-solving and administrative resilience.

#### Step 2: Build and Execute Advanced Filtered API Queries
Using the terminal, I formulated an advanced structural query targeting the Amazon EC2 endpoint. Instead of calling a generic description command that pulls verbose, multi-page data logs, I constructed a precise JMESPath filter to extract only three essential operational attributes: the unique machine identifier, the real-time lifecycle state, and the hardware class family.

The optimized command string was executed as follows:
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name,InstanceType]" --output table
Step 3: Analyze and Validate the Tabular Infrastructure State Output
The API gateway processed the authenticated request and returned a structured text matrix, completely bypassing raw JSON bloat. The terminal output displayed the active lab machine with its Instance ID (i-058d40dc31f87c225), an active operational lifecycle state (running), and the instance type classification (t2.micro), validating that the cloud infrastructure was running properly under direct command-line control.

🧠 Key Insights & Engineering Takeaways
Hybrid Architecture Realities: Designing hybrid networks demands a deep understanding of split-horizon routing. Inbound and Outbound Endpoints are not merely configuration options; they represent dedicated network bridges that require deliberate subnet layout and multi-AZ positioning to avoid enterprise-wide DNS blackouts.

Operational Problem Solving: Operational workflows in the cloud are rarely perfectly linear. When managed cloud services like AWS CloudShell face regional restrictions or verification locks, a systems engineer must pivot quickly—either by switching execution environments, configuring local terminal proxies, or leveraging alternative shell contexts to keep deployments on track.

Lifecycle Discipline & Cost Control: Automated cloud environments demand strict compliance with resource lifecycle management. Leaving unused infrastructure active—especially network-intensive components like Route 53 Resolver Endpoints or unattached Elastic IPs—leads to unnecessary operational costs. Establishing a systematic creation, validation, and deletion routine is a fundamental habit of an efficient cloud professional.

🚀 Looking Ahead: Week 5 Goals & Milestones
To maintain momentum within the First Cloud AI Journey – Workforce Bootcamp 2026 program, my objectives for Week 5 will pivot toward infrastructure security, multi-tier network boundaries, high-performance load balancing, and global content delivery.

📋 Planned Lab Modules:
Lab 13: Advanced VPC Topology - Building an Advanced VPC Topology with Multi-Tier Subnet Distribution to isolate database layers from web instances.

Lab 14: Elastic Load Balancing - Establishing Elastic Load Balancing (ELB) for automated incoming application traffic management.

Lab 15: Auto Scaling Groups - Implementing Auto Scaling Groups (ASG) to ensure dynamic system elasticity and fault tolerance based on real-time traffic load.

Lab 16: Amazon CloudFront - Configuring Amazon CloudFront for low-latency global content delivery via regional edge caches.

📅 Event Attendance:
In addition to completing the advanced lab technical modules, I plan to attend the 2nd Official Bootcamp Event hosted at the AWS Vietnam Office (Bitexco Financial Tower). This corporate session will provide essential opportunities to sync with cloud solutions architects, evaluate production-grade enterprise deployment frameworks, and strengthen community networking ties with industry professionals.