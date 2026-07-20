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


## Deep-Dive Research Directory

### Blog 1 - Scaling to 1 Million AWS Lambda Functions

**Article**

[Scaling to 1 Million AWS Lambda Functions: Hard-Earned Lessons on Massive-Scale Serverless Architecture](./3.1-Blog1/)

This article explains how AWS designs highly scalable Serverless systems using Event-Driven Architecture. It focuses on asynchronous workloads, service quotas, and workflow orchestration.

**Architecture Pattern:** Event-Driven Architecture & Workflow Orchestration

**Core AWS Services:** AWS Lambda | Amazon SQS | AWS Step Functions | AWS SAM | AWS CloudFormation

---

### Blog 2 - Pinterest Multi-Account Transformation

**Article**

[From Monolith to Multi-Account: Pinterest's Total AWS Organization Transformation Journey at Scale](./3.2-Blog2/)

This article summarizes Pinterest's migration from a single AWS account to a centralized multi-account environment. It highlights governance, security, and operational best practices for large-scale cloud environments.

**Architecture Pattern:** Multi-Account Strategy & Centralized Cloud Governance

**Core AWS Services:** AWS Organizations | AWS Control Tower | AWS IAM Identity Center | AWS Config | Amazon CloudTrail

---

### Blog 3 - Authentication & Session Management

**Article**

[Building a Modern Authentication and Session Management Service with Amazon Aurora DSQL](./3.3-Blog3/)

This article describes how AWS builds a scalable authentication and session management service using Amazon Aurora DSQL. It emphasizes secure credential handling, strong read-after-write consistency, and the benefits of managed serverless services.

**Architecture Pattern:** Serverless Backend Architecture & Authentication Service

**Core AWS Services:** Amazon Aurora DSQL | Amazon ECS Express Mode | AWS Fargate | AWS IAM | Amazon CloudWatch

</div>