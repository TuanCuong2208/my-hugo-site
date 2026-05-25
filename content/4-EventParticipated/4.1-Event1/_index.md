---
title: "Event 1"
date: 2026-05-24
weight: 1
chapter: false
pre: "<b>4.1. </b>"
---

# EVENT REPORT: "FCAJ COMMUNITY DAY WORKSHOP"

* **Time:** 09:00 AM – 12:00 PM, Saturday, May 23, 2026
* **Location:** Floor 26, Bitexco Financial Tower, 02 Hai Trieu Street, Ben Nghe Ward, District 1, Ho Chi Minh City
* **Role:** Attendee
* **Author:** Nguyen Tuan Cuong - Final-year Software Engineering Student (HUTECH)

---

### Event Objectives
* Share production-ready best practices for designing and deploying modern application architectures on the AWS Cloud platform.
* Introduce Domain-Driven Design (DDD) methodologies and Event-Driven Architectures (EDA) within enterprise environments.
* Provide comprehensive guidelines for selecting and optimizing compute services to balance infrastructure scalability and operational costs.
* Introduce next-generation AI tools designed to enhance efficiency across the entire Software Development Lifecycle (SDLC).

### List of Speakers
* **Ms. Vy Lam** - Senior Business Systems Analyst, VPBank
* **Ms. Thao Nguyen** - GenAI Engineer, VIB
* **Ms. Mai Nguyen** - GenAI Engineer, VIB
* **Ms. Uyen Le** - GenAI Engineer, VIB
* **Mr. Tinh Truong** - Platform Engineer, GoTymeX
* **Mr. Thinh Nguyen** - DevOps Engineer, FCAJ
* **Mr. Duc Dao** - Solutions Architect, Cloud Kinetics
* **Mr. Pham Ng. Hai Anh** - Cloud Consultant, G-AsiaPacific Vietnam

---

### Technical Insights & Presentation Summaries

#### 1. Context Is Everything - Bringing AI to Production (Mr. Tinh Truong - Platform Engineer, GoTymeX)
This session focused on maximizing Large Language Model (LLM) performance through advanced Context Engineering. When implementing AI in production environments, poor or hallucinatory outputs are rarely caused by model limitations; instead, they stem from weakly structured context.
* **Anatomy of an Optimal Context:** A robust context must include four essential elements: the explicit Goal, the real-world Situation, system Constraints, and relevant technical Evidence or source code.
* **3 Common Enterprise Pitfalls:**
  1. *The Internet Puller:* Dumping unorganized, raw documents or entire PDFs into prompts, which creates informational noise and wastes token budgets.
  2. *Repeating Pre-trained Knowledge:* Feeding the model obvious system paradigms it already knows rather than focusing on specific logic refactoring requirements.
  3. *Lack of Technical Constraints:* Providing vague, generic instructions that result in boilerplate outputs incompatible with current production codebases.
* **The Evolution Paradigm:** AI interactions have progressed through three phases: Single Prompts -> Dynamic Context (with attached documents) -> Long-Term Personalized Memory. This architecture lays the foundation for a "Second AI Brain," leveraging Amazon S3 for durable storage, Vector Databases for contextual retrieval, and Amazon Bedrock for managed inference generation.

#### 2. Friendly AI Assistant with Amazon Q (Mr. Pham Ng. Hai Anh - Cloud Consultant, G-AsiaPacific Vietnam)
This presentation addressed the challenge of boosting operational productivity for non-technical enterprise personnel using secure, intelligent automated agents.
* **Agentic AI Mechanisms:** Introduced Amazon Q, which supports more than 40 secure native data connectors linking Amazon S3, corporate relational databases, and trusted third-party enterprise tools into a unified, actionable AI Agent ecosystem.
* **Practical Use-Case (PM Assistant Demo):** Demonstrated an automated pipeline tailored for Project Managers. The AI agent captured live insights, drafted Minutes of Meetings (MoM), generated actionable emails to key stakeholders, and automatically updated schedules for upcoming deliverables.
* **Enterprise-Grade Safeguards:** The implementation enforces strict security Guardrails, precise Access Controls, and compliance with regulatory frameworks to ensure sensitive corporate data never leaks beyond organization boundaries.

#### 3. Maximizing Performance and Security with CloudFront (Mr. Thinh Nguyen - DevOps Engineer, FCAJ)
A deep technical breakdown of architectural strategies used to eliminate unexpected infrastructure bill spikes caused by sudden traffic surges or Distributed Denial of Service (DDoS) attacks.
* **Fixed-Price CDN + Security Package:** Discussed AWS's flat-rate pricing model that bundles Amazon CloudFront, AWS WAF, AWS Shield, Amazon Route53, and S3, allowing enterprises to scale confidently without financial volatility.
* **Advanced Networking Architecture:**
  * *Edge-Level Mitigation:* Utilizing CloudFront's global network of over 700 Points of Presence (PoPs) to intercept and absorb network-layer attacks (such as SYN floods) at the edge, protecting origin infrastructure.
  * *Origin Cloaking:* Completely shielding origin server IP addresses from the public internet using VPC Origin configurations and tight Origin Access Control (OAC) bucket policies.
  * *Protocol Optimization:* Implementing HTTP/3 over QUIC/UDP to allow request multiplexing and eliminate head-of-line blocking. Activating advanced data compression algorithms achieved up to an 82% reduction in bandwidth consumption while maintaining persistent TCP connections to eliminate handshake overhead.
  * *Edge Computing:* Deploying routing logic, URL rewrites, and API mocking directly to the network edge via CloudFront Functions and Lambda@Edge, reducing primary EC2 origin CPU utilization from 5% to under 1%.

#### 4. UTMorpho - From Concept to Product in 36 Hours (LotusHacks 2026 - VIB Engineering Team)
A practical, fast-paced case study tracking the development of a production-ready application under intense time constraints during LotusHacks 2026.
* **Problem & Solution:** To address the repetitive bottlenecks found in standard UI/UX wireframing, the team engineered a neural interface called UTMorpho. Users scan a rough hand-drawn wireframe sketch from paper or an iPad, and the system leverages Claude 4 Sonnet to generate clean, production-ready frontend source code instantly.
* **Hackathon Engineering Challenges:** Managing the risk of AI Overgeneration (bloated, unoptimized source code), avoiding API token throttling under high-frequency testing, and navigating severe team burnout during the intense 36-Hour Sprint.
* **Key Takeaways:** The turning point relied on shifting from an overly broad scope to an intentionally "Focused Editing Experience." Maintaining continuous Team Sync and prioritizing structural features over superficial details were critical to delivering a functioning prototype before the deadline.

#### 5. Navigating Non-Determinism in Large Language Models (Mr. Duc Dao - Solutions Architect, Cloud Kinetics)
A rigorous computer science lecture examining how physical hardware behaviors alter the consistency of generative AI applications.
* **Debunking the Temperature = 0 Myth:** Developers widely assume that setting Temperature to 0 forces the model to select the absolute highest probability token (argmax), guaranteeing a 100% deterministic output across API calls for structured JSON/YAML generation or automated Regression Testing.
* **Empirical Research Findings:** Testing 5 major foundation models (including GPT-3.5, GPT-4o, Llama-3, and Mixtral) across 8 natural language processing (NLP) tasks over 10 identical runs with static seed parameters revealed up to a 15% variance in accuracy between executions. The strict string matching rate (TARr@10) dropped to nearly 0% on advanced logical reasoning tasks.
* **Hardware-Level Root Causes:** Floating-point arithmetic executed in parallel across modern GPU clusters is inherently non-associative under the IEEE 754 standard. Minor variations in thread execution order on parallel hardware introduce micro-rounding errors in logits, altering the argmax token selection. Concurrently, request batching algorithms used by API providers to optimize GPU compute dynamically alter the execution environment.
* **Mitigation Strategies:**
  * Implementing Majority Voting or Ensemble architectures across multiple independent executions to prioritize accuracy over raw compute costs.
  * Forcing strict structured schemas at the system level via native JSON Mode, function calling, or regex constraints.
  * *Production Tip:* Pure T=0 settings frequently lock models into endless, repetitive vocabulary loops. The ideal practical sweet spot is **T=0.1**, which provides near-deterministic behavior while introducing enough stochastic variance to prevent logical deadlocks.

#### 6. Enterprise-Grade Multi-Agent Systems in Corporate Credit Scoring (Ms. Vy Lam - Senior BSA, VPBank)
An architectural deep dive into a production-grade Multi-Agent AI system deployed in commercial banking to automate corporate credit risk assessments for early-stage startups.
* **The Business Challenge:** Startups operate on thin historical data (6–18 months) and lack the 3-year audited financial records or physical collateral required by traditional commercial banking models, despite possessing high-value intellectual property (IP) and rapid growth trajectories.
* **Multi-Agent vs. Single Agent Architectures:** Single AI Agent implementations fail due to context window limits, specialized domain dilution, and a lack of built-in cross-verification. The proposed solution deploys a **Virtual Credit Committee** built on a Multi-Agent framework. Specialized agents run in parallel, including a *Manager Agent, Financial Analyst Agent, Market Analyst Agent, Team Evaluator Agent,* and *Risk Assessor Agent*. These agents hold cross-functional debates, generating a transparent Audit Trail and strengthening system Fault Tolerance.
* **6 Pillars of Enterprise-Grade Design:** Moving AI from local testing to production banking requires strict adherence to six foundational pillars: comprehensive data security (IAM roles, KMS encryption, secret rotation), Data Governance (strict residency and automated PII masking), Network Isolation (isolated VPCs, AWS PrivateLink), Observability (Prometheus/Grafana logging, Auto-scaling profiles), Human-in-the-loop validation, and compliance with global standards (SOC 2, GDPR, PCI DSS).
* **Granular Guardrail Engineering:** Implementing a 3-layer defensive wrapper consisting of *Input Guardrails* (preventing prompt injection), *Processing Guardrails* (monitoring runtime timeouts and token spend), and *Output Guardrails* (detecting and filtering semantic hallucinations).
* **Enterprise Cloud Deployment Pipeline:** Code developed locally using the CrewAI framework -> Packaged into Docker Images -> Uploaded to AWS ECR -> Orchestrated via Bedrock AgentCore with AWS Lambda integration -> Exposed securely through AWS API Gateway.
* **Business Performance & ROI:** Reduced corporate credit underwriting turn-around time by 95% (from 2–3 weeks down to 2–4 hours). Increased scoring accuracy and approval yields from 35% to 45%. Lowered operational processing costs per application from ~100 million VND to under 5 million VND, delivering a full investment payback period within 12–15 months.

---

### Conclusion & Future Learning Roadmap
Attending this AWS Community Day served as a powerful wake-up call for me as an IT student. In university, projects often conclude once the code simply runs as a Proof of Concept. However, real-world production—particularly regarding Cloud and AI systems—demands an entirely different enterprise-grade engineering approach.

I realized that:
* &emsp;**Core foundational knowledge is critical:** AI will not replace software developers. Mastering the underlying floating-point architecture of GPUs or networking protocols like HTTP/3 and continuous TCP handshakes is the ultimate key to controlling the technology rather than just consuming APIs.
* &emsp;**System design skills are paramount:** VPBank’s Multi-Agent architecture illustrates how future software design will resemble decentralized microservices, where specialized AI agents collaborate, balance, and cross-examine one another.
* &emsp;**Security and Context are King:** For AI to become truly viable within enterprise spaces, mastering Context Engineering and deploying rigorous security isolation layers (VPCs, OACs, and Multi-layered Guardrails) is mandatory to guarantee sensitive production data remains safe from leaks.

This worklog goes beyond a standard event recap; it provides a direct technical framework for my upcoming graduation thesis: building an AI application that is not only intelligent but structurally secure, cost-optimized, and resilient under an enterprise-level model. Thank you to the speakers and AWS for providing such an outstanding technical event! I will immediately begin exploring the Model Context Protocol (MCP) and Terraform infrastructure tooling as recommended by the panels.