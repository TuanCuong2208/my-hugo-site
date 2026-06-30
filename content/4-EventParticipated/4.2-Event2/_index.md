---
title: "Sự kiện 1"
date: 2026-06-30
weight: 2
chapter: false
pre: "<b>4.1. </b>"
---

# REPORT ON "FCAJ COMMUNITY DAY WORKSHOP"

* **Time:** 09:00 - 12:00, Saturday, June 27, 2026
* **Location:** 26th Floor, Bitexco Financial Tower, 02 Hai Trieu, Ben Nghe, District 1, Ho Chi Minh City
* **Role:** Attendee
* **Author:** Nguyen Tuan Cuong - Final-year Software Engineering Student (HUTECH)

---

### Event Objectives
* Share production-grade best practices in designing and architecting modern applications on the AWS cloud platform.
* Introduce Domain-Driven Design (DDD) methodologies and Event-Driven Architecture (EDA) paradigms within enterprise environments.
* Guide and optimize the selection process of appropriate cloud compute services aligned with scalability requirements and infrastructure cost efficiency.
* Introduce next-generation generative AI tools supporting the entire Software Development Lifecycle (SDLC).

---

## PRESENTATION OVERVIEW

The tech workshop "FCAJ Community Day - June 2026" focused heavily on leveraging next-generation Artificial Intelligence (AI) to solve operational, automation, and workforce management challenges in large-scale enterprise environments. Below is the detailed presentation timeline for the speaker groups based on the official event agenda:

| Timeline | Presenting Group | Main Topic |
| :--- | :--- | :--- |
| **09:00 - 09:25 AM** | Group 1 | Deep Response Engine: From Detection to Autonomous Resolution |
| **09:25 - 09:55 AM** | Group 2 | Voice Agents: Building Human-Like AI Conversations at Scale |
| **09:55 - 10:20 AM** | Group 3 | AWS DevOps Agent: Your Always-Available Operations Teammate |
| **10:20 - 10:45 AM** | Group 4 | AI-Powered Productivity: Workforce Planning For Enterprise |
| **10:45 - 11:30 AM** | Group 5 | Building Secure Private MCP Connection with Amazon Quick |

---

## DETAILED SPEAKER GROUP SESSIONS

### 🛠️ Group 1: Deep Response Engine: From Detection to Autonomous Resolution
* **Speaker:** Steve Tran (Cloud Thinker)
* **Technical Insights:**
    * Focused on **Agentic AI** solutions designed for autonomous incident response across Cloud Infrastructure.
    * Provided an in-depth comparison between **Single Agent and Multi-Agent** architectures, demonstrating how Multi-Agent designs optimize the *Context Window* and offer superior *Role-Based Access Control (RBAC)*.
    * Integrated **FinOps** frameworks for AWS cost optimization alongside comprehensive **Security** measures, emphasizing automated pen-testing of source code, logs, and infrastructure configurations prior to production deployment.
* **Real-world Application:** Signficantly slashes DevOps and SRE overhead costs for enterprise-level organizations (such as major Banks and FPT), accelerating widespread system debugging down to mere minutes.

---

### 🎙️ Group 2: Voice Agents: Building Human-Like AI Conversations at Scale
* **Speakers:** Representatives from Renova Cloud, Student Video Group, and R AI
* **Technical Insights:**
    * Developed native Vietnamese-optimized conversational AI systems (**Voice Agents**) running at enterprise scale.
    * Rather than using direct Speech-to-Speech models, the team architected a decoupled 3-tier system: **STT (Speech-to-Text) $\rightarrow$ LLM (Large Language Model) $\rightarrow$ TTS (Text-to-Speech)** to optimize compute resource allocation and safeguard generation quality.
    * Engineered ultra-low latency real-time streaming data pipelines combined with advanced **Tool Calling** capabilities to handle transactional operations (e.g., executing immediate bank card freezing commands).
    * Advanced localization features: Accurate gender detection for natural honorific pronouns (anh/chị), seamless interrupt handling, and robust regional accent recognition.
* **Real-world Application:** Deployed automated virtual contact centers and debt-collection voice bots for prominent financial institutions like VPBank and VIB; features automatic fallback routing to live human agents when queries escalate past AI processing boundaries.

---

### 🤖 Group 3: AWS DevOps Agent: Your Always-Available Operations Teammate
* **Speakers:** Ms. Bao and Nguyen Nguyen (Cloud Kinetics)
* **Technical Insights:**
    * Engineered a 24/7 autonomous AI assistant specialized in continuous Root Cause Analysis (RCA) for complex infrastructure failures.
    * Introduced the concept of **Agent Space**, which establishes precise infrastructure access boundaries using resource Tags and secure *Private Connections*.
    * Utilized structural context learning to autonomously map and interpret architecture topologies involving AWS Application Load Balancers (ALB), Amazon ECS, and AWS IAM policies.
    * Integrated the open-source **MCP (Model Context Protocol)** to seamlessly query and ingest telemetry from isolated, siloed proprietary data systems.
    * Standardized operations into a clear 4-step workflow: **Classification $\rightarrow$ Investigation $\rightarrow$ Remediation Proposal $\rightarrow$ Infrastructure Improvement Suggestion**.
* **Real-world Application:** Effectively eliminates Fragmented Telemetry and Context Loss across distributed infrastructures; dramatically minimizes Mean Time to Resolution (MTTR) from hours to minutes, while maintaining a **Human-in-the-loop** guardrail for final execution approvals.

---

### 📊 Group 4: AI-Powered Productivity: Workforce Planning For Enterprise
* **Speaker:** Representative from Noventis
* **Technical Insights:**
    * Employed tailored AI capabilities derived from **Amazon Quick** solutions to drive comprehensive digital transformation within enterprise Human Resources (HR) departments.
    * Leveraged **Amazon Quick Skills** to provision custom AI skill sets using natural language configuration files (no-code instructions), natively integrating with Microsoft Outlook, SharePoint, Google Workspace, Jira, and Salesforce.
    * Implemented advanced **OCR** pipelines to systematically scan, parse, and extract applicant data from raw PDF/Doc resume files.
    * Enforced stringent corporate data security policies by executing workloads within **AWS Local Zones in Vietnam**, ensuring sensitive corporate data remains isolated from public AI models.
* **Real-world Application:** Eradicates tedious manual resume screening, performs high-fidelity semantic matching between applicant capabilities and Job Descriptions (JDs), and heavily reduces enterprise *Time to Hire* metrics.

---

### 🔒 Group 5: Building Secure Private MCP Connection with Amazon Quick
* **Speaker:** Toan Nguyen (AWS Security Builder)
* **Technical Insights:**
    * Addressed critical security architecture frameworks to establish a highly secure connection from an **MCP Server** hosted on Amazon Quick to messaging platforms and internal software ecosystems like Zalo, Jira, and custom in-house applications.
    * Mitigated severe vulnerability vectors such as Denial of Service (DoS) and Man-in-the-Middle (MitM) attacks over the public internet by fully enclosing and isolating the MCP Server within a **Private Subnet**.
    * Outlined a multi-layered security model leveraging **AWS VPC Connections**, **Amazon Route 53 Resolver (Internal DNS)** for private domain resolution, and traffic routing via an Application Load Balancer (ALB) integrated with **AWS Certificate Manager (ACM)** for full end-to-end SSL/TLS data encryption.
* **Real-world Application:** Empowers autonomous AI agents to extract highly sensitive corporate data with ironclad security; notes critical architectural considerations regarding auxiliary costs (Data Transfer rates, ALB provisioning, and Route 53 query expenses).

---

## SUMMARY & KEY TAKEAWAYS

Reflecting on the "FCAJ Community Day" workshop sessions, I have consolidated 4 core trends and lessons vital for my upcoming engineering path:

1. **The Evolution of Autonomous AI Agents:** AI technology has fundamentally shifted from reactive chatbot architectures to fully **Autonomous** operational entities characterized by specialized Multi-Agent designs, DevOps Agents, and native **Tool Calling** functionalities.
2. **Private Networking is Mandated for Enterprises:** Setting up orchestration protocols like MCP inside Private Subnets via VPC Connections is a baseline requirement to safeguard corporate environments against public internet attack vectors.
3. **The Human-in-the-loop Paradigm:** AI operates as a powerful teammate to maximize productivity and lower MTTR, rather than a total human replacement. Crucial remediation steps and structural modifications still dictate absolute sign-offs from human engineers.
4. **Breaking Language and Ecosystem Barriers:** Seamlessly combining STT-LLM-TTS pipelines solves intricate Vietnamese localization bugs, while multi-platform integrations (Jira, Salesforce, Zalo...) allow AI to effectively integrate into everyday real-world business workflows.