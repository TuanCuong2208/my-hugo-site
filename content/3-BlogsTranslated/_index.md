---
title: "Team Research Publications"
date: 2026-06-30
weight: 3
chapter: true
pre: "<b>3.</b>"
---

<style>
.publication-page{
    text-align:left !important;
    width:100%;
}

.publication-page h1,
.publication-page h2,
.publication-page h3,
.publication-page h4,
.publication-page p,
.publication-page div,
.publication-page ul,
.publication-page ol,
.publication-page li{
    text-align:left !important;
}

.publication-page hr{
    margin:25px 0;
}
</style>

<div class="publication-page">


<h1 style="text-align:center !important;">Team Research Publications</h1>

During my internship, I regularly studied technical articles published by AWS and other engineering teams. Besides completing AWS Academy labs, I summarized several publications to better understand cloud-native architectures, distributed systems, and engineering best practices.

This page collects the research notes and article summaries completed throughout my internship.

## In-Depth Research Articles

### Article 1 - Scaling to 1 Million AWS Lambda Functions: Hard-Earned Lessons on Large-Scale Serverless Architecture
[Read more here](./3.1-Blog1/)

**Summary:** This article focuses on scaling performance and managing asynchronous workloads at the scale of millions of concurrent functions. By analyzing AWS Service Quotas, the research team highlights how to eliminate traditional anti-patterns, prevent bottlenecks, and build a proactive fail-safe architecture.  
**Applied Architecture:** Event-Driven Architecture & Workflow Orchestration  
**Core AWS Services:** AWS Lambda | Amazon SQS | AWS Step Functions | AWS SAM | AWS CloudFormation

---

### Article 2 - From Monolith to Multi-Account: Pinterest’s Comprehensive AWS Organizations Restructuring Journey at Scale
[Read more here](./3.2-Blog2/)

**Summary:** This article analyzes challenges such as API limits, reducing blast radius, and strengthening system safety. The research team explains how to design Organizational Units (OU), apply centralized control policies to optimize costs, and manage identities at scale.  
**Applied Architecture:** Multi-Account Strategy & Centralized Governance  
**Core AWS Services:** AWS Organizations | AWS Control Tower | IAM Identity Center | AWS Config | Amazon CloudTrail

---

### Article 3 - Building an Authentication and Session Management Service with Amazon Aurora DSQL
[Read more here](./3.3-Blog3/)

**Summary:** This article introduces how to build a modern Authentication and Session Management service using Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate, and IAM Authentication. It emphasizes strong read-after-write consistency, secure session token protection, safe credential management, and scalable backend design with managed/serverless services.  
**Applied Architecture:** Serverless Backend Architecture & Authentication Service  
**Core AWS Services:** Amazon Aurora DSQL | Amazon ECS Express Mode | AWS Fargate | AWS IAM | Amazon CloudWatch
Watch


</div>