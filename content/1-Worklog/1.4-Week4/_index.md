---
title: "Week 4: Container Ecosystem, Automated Enterprise CI/CD and Advanced Hybrid Networking"
date: 2026-05-12
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

# Week 4: Mastering Container Orchestration Duos, DevSecOps Lifecycle Automation and Hybrid Cross-VPC Mesh Architectures

### I. Executive Summary
This week marks a major strategic milestone in my internship journey at AWS Vietnam. I have completely pivoted from traditional virtual server administration mindsets into the era of Application Modernization. The practical research matrix comprehensively covers 7 enterprise-scale Labs: from serverless microservices orchestration (Lab 16), cross-platform automated continuous delivery pipelines (Lab 17, Lab 23), centralized security posture governance through AWS Security Hub (Lab 18), to engineering hybrid cross-VPC communication topologies over wide areas (Lab 19, Lab 20), and Event-Driven infrastructure cost optimization using automated triggers (Lab 22).

### II. Strategic Objectives of the Week
* **Application Modernization via Containers (Microservices Orchestration):** Master the technical skills of packaging, segregating, and coordinating decoupled Frontend/Backend service clusters using Amazon ECS Fargate Serverless.
* **Standardizing Full-Stack DevSecOps Lifecycles (Automated CI/CD Pipelines):** Construct robust pipelines to automate software testing, compilation, and continuous deployment from remote GitLab repositories or GitHub Actions directly into ECS Container clusters and EC2 environments using the AWS Code Suite stack.
* **Centralized Security Governance & Compliance Baseline (Enterprise Security Governance):** Activate AWS Security Hub to continuously audit and score cloud infrastructure compliance against strict international cybersecurity standards.
* **Engineering Complex Multi-VPC Topologies (Hybrid Cross-VPC Mesh):** Master isolated network peering techniques via VPC Peering and centralize high-scale routing architectures using AWS Transit Gateway.
* **Serverless Financial Operations (Serverless Cost Optimization):** Deploy AWS Lambda coupled with CloudWatch Rules to automatically toggle infrastructure runtime states based on cron schedules, eliminating non-production idle spending leakages.

---

### III. Activity Log & Detailed Roadmap (From 12/05/2026 to 18/05/2026)

| Timeframe | Activity Category | In-depth Operational Tasks Executed | Results / Deliverables Achieved |
| :--- | :--- | :--- | :--- |
| **Day 1** *(12/05)* | Container Orchestration | Deploy Lab 16: Configure ECS Cluster, Task Definitions, and multi-tier Frontend/Backend services running on AWS Fargate Serverless. | Microservices stack establishing secure cross-tier communication via internal Service Discovery. |
| **Day 2** *(13/05)* | CI/CD Automation | Deploy Lab 17: Establish continuous integration and automated deployment flows from GitLab/GitHub Actions directly to ECS Container clusters. | End-to-end software delivery pipeline working seamlessly without manual engineering interventions. |
| **Day 3** *(14/05)* | Centralized Security | Deploy Lab 18: Activate AWS Security Hub, conduct vulnerability assessment scans, and evaluate the automated posture compliance score. | Comprehensive enterprise cloud security audit and monitoring baseline established. |
| **Day 4** *(15/05)* | Cross-VPC Routing | Deploy Lab 19: Establish VPC Peering connections between two completely isolated virtual networks and customize core Route Tables. | Internal network packets traversing secure cross-VPC tunnels with optimal low latency. |
| **Day 5** *(16/05)* | Hub-and-Spoke Networking | Deploy Lab 20: Initialize AWS Transit Gateway, attach a network of 4 isolated VPCs, and segregate centralized route domains. | Eradicated messy mesh connectivity architectures, optimizing enterprise network administration. |
| **Day 6** *(17/05)* | FinOps Cost Optimization | Deploy Lab 22: Program AWS Lambda execution scripts triggered by CloudWatch Rules to automatically shut down/start up EC2 hosts on a schedule. | Event-driven architecture automatically minimizing non-production resource idle hours. |
| **Day 7** *(18/05)* | Native CI/CD & Portfolio | Deploy Lab 23: Architect an AWS native CodePipeline. Aggregate documentation assets, audit media paths, and publish the Worklog. | Week 4 activity log running fully live and healthy on the custom Hugo portfolio portal. |

---

### IV. Technical Deep Dives & Detailed Analysis of the Labs

#### **1. Lab 16: Deploy Applications on Amazon Elastic Container Service (Amazon ECS)**

##### **Overview**
In the modern cloud era, operating applications depending on standalone EC2 virtual servers constantly reveals massive limitations regarding scaling speed, environment consistency, and the administrative burden of OS patching. This Lab definitively addresses this problem by modernizing a real-world two-tier enterprise application, packaging the entire frontend user interface code base and backend business logic layer into isolated Docker Containers, under the absolute orchestration of **Amazon ECS** on the serverless compute engine **AWS Fargate**.

##### **Core Technical Concepts**
* **Amazon ECS Cluster Fargate:** A logical grouping of resources designated to run container workloads. The ultimate superiority of Fargate is the complete elimination of visible EC2 virtual server instances inside the account, delegating the hardware allocation layer to AWS for automatic management, thereby elevating peripheral boundary security to the absolute maximum.
* **Task Definition Topology:** A detailed blueprint specifying exactly how containers should behave (analogous to a local `docker-compose.yml` file). It explicitly declares the ECR Image URI, enforces strict resource constraints at the bare minimum to conserve budget (`0.25 vCPU` and `0.5 GiB RAM`), and injects connectivity configuration environment variables.
* **Service Discovery & AWS Cloud Map:** Since Serverless containers dynamically scale and recreate frequently, their internal IP addresses constantly drift. The architecture integrates AWS Cloud Map natively coupled with Route 53 to seamlessly update internal DNS records (`ecs.local`). This allows the Frontend tier to reliably call the Backend tier's APIs without losing the network routing path.

##### **Step-by-step Execution**

###### **Step 1: Initializing the orchestration Cluster and designing internal network Namespaces**
I accessed the Amazon ECS console and initiated a centralized orchestration cluster named `Production-Cluster` running entirely on the Fargate Engine. The creation workflow concurrently activated the AWS Cloud Map automated network identifier, registering the system Namespace as `ecs.local` to serve as the structural foundation for downstream cross-tier container Service Discovery.
<img src="/images/week3/1.png" alt="Khởi tạo cụm điều phối Amazon ECS Cluster và cấu hình Namespace" style="max-width:100%; height:auto;" />

###### **Step 2: Scripting the Task Definition manifests for microservices components**
I proceeded to configure the Task Definition blueprint for the Backend Service Container. Inside the environment variables configuration block, I declared the exact connection strings and security credentials pointing directly to the Amazon RDS MySQL core database setup from Week 2, establishing strict hardware limitations to safely maintain the account within Free Tier boundaries.
<img src="/images/week3/2.png" alt="Cấu hình thông số Task Definition cho Backend Service Container" style="max-width:100%; height:auto;" />

###### **Step 3: Deploying ECS Services and auditing Task lifecycles**
I triggered the activation of ECS Services for both application tiers, configuring the desired task count to execute independently in the background. Navigating to the Tasks management tab to monitor the rollout, the system recorded that the container entities successfully pulled the images from the ECR repository and shifted their states simultaneously to a stable green (**`RUNNING`**).
<img src="/images/week3/3.png" alt="Giám sát danh sách các Container Task hoạt động ở trạng thái Running" style="max-width:100%; height:auto;" />

###### **Step 4: Validating multi-tier cross-connection integrity via ALB Endpoint**
To thoroughly audit the validity of the infrastructure stack, I extracted the public DNS Endpoint address of the Application Load Balancer (ALB) and accessed it through my local web browser. The administrative interface rendered data smoothly, confirming that the Frontend Container successfully resolved the DNS path to call the Backend Container, which successfully executed data read/write queries against the core RDS MySQL Database.
<img src="/images/week3/4.png" alt="Xác thực ứng dụng Microservices trên cụm ECS hoạt động thành công trên trình duyệt" style="max-width:100%; height:auto;" />

---

#### **2. Lab 17: Deploying CI/CD with ECS Container - Automating Cross-Platform Microservices Delivery Pipelines**

##### **Overview**
Manually managing and deploying source code alterations onto an active Container infrastructure cluster constantly exposes operations to critical human errors and wastes significant engineering hours. This Lab concentrates on materializing an automated software supply chain model leveraging **CI/CD (Continuous Integration/Continuous Deployment)**. The system is architected to fully automate every stage: from intercepting code push trigger events, packaging Docker Images, pushing to the Amazon ECR registry, to seamlessly updating Task Definitions to trigger Zero-Downtime Deployments on Amazon ECS.

##### **Core Concepts**
* **Continuous Integration and Continuous Deployment (CI/CD):** An automated system framework designed for software delivery. Any source code adjustments committed or pushed to the Git repository instantly trigger the pipeline engine to validate, compile, and publish the application assets.
* **Cross-Platform Delivery Pipelines (GitLab CI & GitHub Actions):** Harnessing the procedural execution power of configuration scripts (such as `.gitlab-ci.yml` or `deploy.yml`) to bifurcate the lifecycle: A Build Stage running Docker build directives, and a Deploy Stage invoking AWS APIs to update active ECS services.
* **AWS CodeBuild Integration:** A fully-managed cloud compilation service that dynamically spins up ephemeral, on-demand compute resources to compile code and automatically tears them down upon completion to achieve maximum cost efficiency.

##### **Step-by-step Execution**

###### **Step 1: Establishing environment access control and secret credentialing (IAM Roles)**
To empower external delivery runners (GitLab Runners, GitHub Actions Enterprise) to interact securely with the AWS cloud platform, I initialized a dedicated IAM User restricted specifically to ECR registry writes and ECS deployment update capabilities. The cryptographic credentials `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` were safely injected and encrypted into the *Variables / Secrets* vault of the remote Git repository.
<img src="/images/week4/5.png" alt="Configuring secure environment access secrets on Git Repository" style="max-width:100%; height:auto;" />

###### **Step 2: Scripting automated Docker Image packaging and registry pushes**
I proceeded to construct the Pipeline definition file for the target project. The orchestration script was programmed to execute the `docker build` statement to wrap the raw source code into a standardized artifact, subsequently calling the secure remote ECR registry login API (`aws ecr get-login-password`) and pushing the freshly minted image file to the centralized ECR repository tagged with the Git commit hash.
<img src="/images/week4/6.png" alt="Scripting the CI/CD build block and pushing Docker Image to ECR" style="max-width:100%; height:auto;" />

###### **Step 3: Integrating AWS CodeBuild and engineering automated Infrastructure updates**
For the native AWS delivery pathway, I configured **AWS CodeBuild** to orchestrate the backend build server operations. The `buildspec.yml` execution manifest was optimized to dynamically generate an output file named `imagedefinitions.json` after compilation, directly mapping the fresh image digest tag onto the corresponding ECS Fargate Task block.
<img src="/images/week4/7.png" alt="Configuring the automated compilation project via AWS CodeBuild interface" style="max-width:100%; height:auto;" />

###### **Step 4: Validating automated Rolling Update behaviors on Amazon ECS**
Upon pushing a fresh user interface modification to the remote repository, the pipeline automation immediately kicked off. Auditing the Amazon ECS Management Console, the target ECS Service entered a secure Rolling Update lifecycle state: An existing Task was temporarily kept active to handle inbound client traffic while a new Task hosting the revised container code base was spun up concurrently. Once the integrated Health Check confirmed a healthy node status, the obsolete Task was automatically terminated, completing a 100% automated software lifecycle upgrade.
<img src="/images/week4/8.png" alt="Validating automated Task lifecycle rollouts on Amazon ECS infrastructure" style="max-width:100%; height:auto;" />

---

#### **3. Lab 18: Getting Started with AWS Security Hub - Centralized Security Posture Governance and Compliance Baseline**

##### **Overview**
As the scale of resources and distributed cloud services expands, manually monitoring configuration flaws or vulnerabilities across isolated infrastructure endpoints becomes entirely unfeasible. This Lab concentrates on initializing and orchestrating **AWS Security Hub**. Acting as the central focal point of supreme security governance, it fully automates the process of collecting, normalizing, and prioritizing security alerts generated by core security services (such as Amazon GuardDuty, Amazon Inspector, Amazon Macie) as well as integrated partner solutions to deliver an aggregated defensive posture view.

##### **Core Concepts**
* **AWS Security Hub:** A Cloud Security Posture Management (CSPM) service that aggregates and normalizes security alerts (Findings) into an interactive and centralized graphical dashboard.
* **Security Standards Baseline:** Automated configuration test suites that evaluate infrastructure compliance against rigorous international cybersecurity standards such as **AWS Foundations Security Best Practices** and the **CIS AWS Foundations Benchmark**.
* **Compliance Posture Score:** A mathematically precise percentage (%) score reflecting the account’s safety level based on passing automated checks, enabling engineers to instantly spot infrastructure weaknesses for automated or manual remediation.

##### **Step-by-step Execution**

###### **Step 1: Enabling the centralized AWS Security Hub management engine**
I navigated to the centralized **AWS Security Hub** service console and executed the primary enablement workflow, prompting the cloud infrastructure to spin up required service-linked roles and initialize the auditing backbone.
<img src="/images/week4/9.png" alt="Enabling AWS Security Hub Console" style="max-width:100%; height:auto;" />

###### **Step 2: Subscribing to international cybersecurity compliance standards**
Under the standards subscription management interface, I enabled the core security frameworks: *AWS Foundational Security Best Practices* and *CIS AWS Foundations Benchmark*. This signals the system to execute background automated compliance checks across all resource clusters.
<img src="/images/week4/10.png" alt="Selecting Target Compliance Security Standards" style="max-width:100%; height:auto;" />

###### **Step 3: Analyzing the centralized Dashboard and evaluating compliance scoring metrics**
Once the infrastructure scanning sequence reached completion, I audited the main Dashboard view. The interface renders visual analytic charts, classifying security findings by severity from `Low` to `Critical`, while supplying the aggregated compliance score metrics for the target cloud environment.
<img src="/images/week4/11.png" alt="Analyzing the Centralized Compliance Posture Score Dashboard" style="max-width:100%; height:auto;" />

###### **Step 4: Inspecting granular security Findings and planning configuration remediation**
I transitioned to the **Findings** management ledger to filter out high-priority configuration deviations (such as active IAM Users missing MFA or Security Groups exposing sensitive management ports to the world). For each item, Security Hub delivers exact resource paths and prescriptive remediation directions to guide engineers through security patching workflows.
<img src="/images/week4/12.png" alt="Auditing Granular Security Findings and Remediation Paths" style="max-width:100%; height:auto;" />

---

#### **4. Lab 19: Setting Up VPC Peering - Engineering Inter-VPC Interconnections and Routing Topologies**

##### **Overview**
By default, standalone Amazon VPC virtual networks deployed within the AWS Cloud environment are entirely isolated and lack the capacity to communicate directly with one another. This Lab concentrates on establishing and orchestrating a **VPC Peering** connection between two separate VPCs. This networking capability provisions a secure, low-latency, point-to-point routing tunnel cutting across private spaces, empowering distributed instances to exchange data directly without traversing the public internet.

##### **Core Concepts**
* **VPC Peering Connection:** A one-to-one logical networking relationship bridging two discrete VPC configurations. This high-performance pathway leverages the private AWS global network backbone, ensuring data traffic remains strictly insulated and never touches the public internet.
* **Non-overlapping CIDR Blocks:** A strict architectural prerequisite for successfully spinning up a peering channel requires that the CIDR IP blocks of both networks do not overlap or intersect (e.g., `172.31.0.0/16` paired with `10.10.0.0/16`) to avert deep packet routing conflicts.
* **Bidirectional Routing Integration:** Establishing the peering bridge merely provisions the logical network channel. To actually flow IP packets, engineers must manually inject clear reciprocal route paths into the Route Tables of both VPCs, mapping the foreign target CIDR block onto the newly generated Peering Connection target ID (`pcx-xxxx`).

##### **Step-by-step Execution**

###### **Step 1: Initiating the cross-network Peering Connection creation request**
I navigated to the virtual networking VPC management dashboard, accessed the **Peering connections** section, and initiated a fresh request. I declared my primary lab deployment VPC as the Requester entity and targeted the exact asset ID of the secondary destination VPC as the Accepter entity before launching the creation trigger.
<img src="/images/week4/13.png" alt="Initiating the Peering Connection Creation Request" style="max-width:100%; height:auto;" />

###### **Step 2: Accepting the inbound peering request and validating Active state status**
Pivoting over to the target destination network scope, I inspected the inbound connection log and executed the **Accept Request** workflow from the Actions dashboard menu. The cloud control plane instantly wired the secure logical routing pipe, shifting the live lifecycle state to **`Active`**.
<img src="/images/week4/14.png" alt="Accepting Inbound Peering Request to Trigger Active Status" style="max-width:100%; height:auto;" />

###### **Step 3: Modifying independent Route Tables to enforce secure bidirectional traffic routing**
To finalize the operational objective, I audited the independent Route Tables bound to the Public Subnet layers of both distinct VPC environments. Under the **Routes** configuration tab, I injected a custom routing statement: defining the remote peer's CIDR block space as the target destination and mapping the target gateway point directly to the live Peering Connection ID.
<img src="/images/week4/15.png" alt="Injecting Peering Connection Statements into Core Route Tables" style="max-width:100%; height:auto;" />

---

#### **5. Lab 20: Set Up AWS Transit Gateway - Engineering Centralized Hub-and-Spoke Enterprise Network Topologies**

##### **Overview**
As the number of isolated Amazon VPC virtual networks expands across an enterprise ecosystem, interconnecting them using a traditional full-mesh topology via individual VPC Peering channels becomes immensely bulky, complex, and unmanageable. With $N$ VPCs, a system grows exponentially, requiring $\frac{N(N-1)}{2}$ discrete peering connections. This Lab definitively mitigates this high-scale challenge by deploying **AWS Transit Gateway (TGW)**. Acting as a centralized network "Hub", this cloud router aggregates and bridges a architecture of **four VPCs** ("Spokes") together, drastically simplifying the network layout and optimizing cross-VPC routing governance from a single pane of glass.

##### **Core Concepts**
* **AWS Transit Gateway:** A highly scalable, fully-managed network transit hub operating as a high-performance cloud Layer 3 router to centralize, orchestrate, and control data traffic flowing across distinct VPCs, remote on-premises VPN infrastructure, and AWS Direct Connect pipelines.
* **Transit Gateway Attachments:** The infrastructure onboarding mechanism used to wire network resources onto a centralized Transit Gateway. This lab executes individual attachments for **four distinct VPCs**, enabling the core gateway to intercept and route transit packets arriving from active subnets.
* **TGW Route Tables & Isolation Control:** Centralized routing domains hosted within the Transit Gateway infrastructure. By segmenting separate route tables and utilizing deliberate route Associations and Propagations, cloud engineers can enforce absolute domain isolation or unlock select cross-VPC communication pathways without modifying individual standalone environments.

##### **Step-by-step Execution**

###### **Step 1: Provisioning the centralized AWS Transit Gateway core routing infrastructure**
I navigated to the virtual networking VPC management dashboard, accessed the **Transit gateways** block, and initiated a fresh deployment named `Hub-TGW`. I established a dedicated Amazon Side Autonomous System Number (ASN) identifier and toggled on the auto-accept sharing property for inbound attachment attachments.
<img src="/images/week4/16.png" alt="Initializing the AWS Transit Gateway Cloud Router Entity" style="max-width:100%; height:auto;" />

###### **Step 2: Attaching the four Spoke VPC networks to the centralized gateway engine**
I transitioned to the **Transit gateway attachments** control ledger to engineer the logical network links for the distributed environments. I executed four standalone attachment routines sequentially: specifying the attachment resource type as *VPC*, targeting the exact ecosystem IDs of the **four VPCs**, and assigning the public subnet layers to act as the primary packet ingress boundaries.
<img src="/images/week4/17.png" alt="Configuring Transit Gateway Attachments to Bridge the Four Spoke VPCs" style="max-width:100%; height:auto;" />

###### **Step 3: Modifying internal VPC Route Tables to implement inward hub-directed routing rules**
To empower virtual computing instances sitting deep within the spoke networks to find their path to the centralized cloud router, I audited the independent internal Route Tables of each respective VPC environment. Under the **Routes** tab, I injected a custom routing statement: defining the target destination IP space of the remote networks and mapping the target gateway output path straight to the central `Transit Gateway` entity to finalize global network connectivity.
<img src="/images/week4/18.png" alt="Updating Local VPC Route Tables to Route Traffic Inwards toward the Transit Gateway" style="max-width:100%; height:auto;" />

---

#### **6. Lab 22: Optimizing EC2 Costs with Lambda - Engineering Event-Driven Serverless Resource Cost Control**

##### **Overview**
Within cloud financial operations framework (FinOps), allowing compute environments (such as non-production Development/Staging virtual servers) to run uninhibited 24/7 during extended idle off-hours (like overnight windows or weekends) incurs significant financial wastage. This Lab addresses this waste by implementing an automated cost-optimization system utilizing an Event-Driven Architecture. By coupling **Amazon CloudWatch Rules (EventBridge)** cron scheduling with an **AWS Lambda** serverless compute function, the infrastructure automates start/stop operational execution lifecycles without human intervention.

##### **Core Concepts**
* **Event-Driven Serverless Computing:** An operational execution framework independent of always-on runtime servers. The Lambda logic only triggers and incurs computational costs per millisecond of calculation upon receiving target event signals.
* **CloudWatch Rules / EventBridge Cron Schedules:** Automation triggers guided by precise cron syntax expressions, responsible for broadcasting periodic execution signals to prompt downstream target functions.
* **Resource Tagging Taxonomy:** The methodology of attaching explicit key-value tracking pairs (e.g., `Environment: Development`) onto targeted EC2 virtual server instances, enabling the backend Lambda code to precisely isolate test assets without cross-contaminating Production workloads.

##### **Step-by-step Execution**

###### **Step 1: Enforcing Resource Instance Tagging and constructing the execution IAM Role**
I injected specific identifying tags onto the target EC2 machine instances intended for financial tracking optimization. Concurrently, within the IAM console, I configured a dedicated IAM Execution Role granting the Lambda platform full programmatic clearance to invoke core API methods: `ec2:StartInstances` and `ec2:StopInstances`.
<img src="/images/week4/19.png" alt="Provisioning the Dedicated Lambda IAM Execution Role Permissions" style="max-width:100%; height:auto;" />

###### **Step 2: Scripting the automated start/stop orchestration logic within AWS Lambda**
I accessed the **AWS Lambda** dashboard console, created a brand-new code node backed by a Python runtime, and bound it to the pre-configured IAM role. I proceeded to craft execution script statements leveraging the native `boto3` SDK library to dynamically sweep instance environments, filter targets possessing the predefined tags, and alter their operational runtime states.
<img src="/images/week3/20.png" alt="Scripting Python Boto3 Logic inside the AWS Lambda Code Block" style="max-width:100%; height:auto;" />

###### **Step 3: Engineering the CloudWatch Cron Trigger and validating automated state transitions**
To finalize the loop, I implemented an automated **CloudWatch Rule** tied to a fixed cron expression target (e.g., stopping instances at 20:00 PM nightly and reviving them at 08:00 AM morning cycles), mapping the execution target output straight to the Lambda module. Upon launching a simulated trigger sequence, the backend gateway responded perfectly: the API calls successfully transitioned targeted development EC2 hosts into a complete stoppage state, while dispatching verification payload messages.
<img src="/images/week3/21.png" alt="Validating Successful Automated Scheduled Instance Lifecycle State Transitions" style="max-width:100%; height:auto;" />

---

#### **7. Lab 23: Deploy Applications to EC2 with AWS CodePipeline - Standardizing Automated Software Delivery via AWS Native Code Suite**

##### **Overview**
Beyond leveraging third-party platforms, the cloud computing ecosystem provisions an integrated native solution stack to build highly secure, fully closed software delivery pipelines that share common IAM access controls. This Lab focuses on materializing an end-to-end automated deployment workflow for a Node.js application running on an EC2 host by seamlessly chaining native cloud services including **AWS CodeCommit**, **AWS CodeBuild**, and **AWS CodeDeploy** under the absolute orchestration of **AWS CodePipeline**.

##### **Core Concepts**
* **AWS CodePipeline:** A fully-managed continuous delivery orchestration service that automates the testing, compilation, and release phases of your application lifecycle based on defined structural workflow stage gates.
* **CodeDeploy Agent & AppSpec Manifest:** A specialized execution daemon residing within the target EC2 instance combined with an `appspec.yml` configuration manifest to govern lifecycle stages, manage package placement, and trigger automated shell scripts during code runtime upgrades.
* **Secure Source Governance (CodeCommit & S3 Artifacts):** A highly secure private Git repository system combined with encrypted transient S3 Buckets to safely pass packaged artifacts between lifecycle stages without exposing intellectual properties.

##### **Step-by-step Execution**

###### **Step 1: Initializing the private internal AWS CodeCommit source repository**
I accessed the CodeCommit administrative panel, created a secure repository named `NodeJS-App-Repo`, and configured credential permissions. I subsequently executed a git push command from my local workstation to sync the Node.js application code base alongside its accompanying `buildspec.yml` and `appspec.yml` deployment files onto the cloud.
<img src="/images/week4/22.png" alt="Initializing and Pushing Code Base to AWS CodeCommit Repository" style="max-width:100%; height:auto;" />

###### **Step 2: Engineering the application deployment infrastructure with AWS CodeDeploy**
I navigated to **AWS CodeDeploy** to provision a deployment Application block and an associated Deployment Group. I targeted the structural deployment matrix by pointing to the custom identifying resource Tags of the destination EC2 instances, defining rolling deployment strategies, and binding the required IAM service roles so the local server daemons could securely receive deployment payloads.
<img src="/images/week4/23.png" alt="Configuring the Targeted Deployment Group within AWS CodeDeploy" style="max-width:100%; height:auto;" />

###### **Step 3: Chaining the complete continuous integration pathway via AWS CodePipeline**
To conclude the loop, I wired an end-to-end **AWS CodePipeline** workflow connecting sequential lifecycles: harvesting code from the *CodeCommit Source Stage*, feeding compiled outputs into the *CodeBuild Stage*, and dispatching finalized artifacts down to the *CodeDeploy Stage*. The automation engine processed the execution sequence smoothly, reporting a complete block transition to a successful state (**`Succeeded`**), rendering the Node.js web application live and accessible on the EC2 host.
<img src="/images/week4/24.png" alt="Validating Succeeded Release Lifecycle Rollouts on AWS CodePipeline Dashboard" style="max-width:100%; height:auto;" />

---

---

### V. Infrastructure Challenges, Error Resolution Logs & Expert Perspectives

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
* **Collaborative Team Meetings & Project Architecture Alignment:** Convene with my university group members to align on our core full-stack graduation project architecture (Vietnam Tour Booking Platform integrated with an AI Chatbot via OpenAI and LangChain). We will benchmark the microservices boundaries, split up code repositories, and map out the AWS infrastructure provisioning plan.
* **Bootcamp Engagement & Event Attendance:** Attend the upcoming workforce bootcamp technical events and technical workshops hosted live at the AWS Vietnam office to consult with Solutions Architects regarding infrastructure design bottlenecks and optimal production packaging patterns.
* **Accumulating Advanced Subject Expertise:** Dedicate specific blocks of time to study engineering lectures and technical video walkthroughs from Solutions Architects on YouTube to update optimal design mindsets, solve performance bottlenecks, and fully prepare for automated application Containerization.