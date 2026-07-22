---
title: "Research Articles"
date: 2026-06-30
weight: 3
chapter: false
pre: "<b>3. </b>"
---

<style>
.publication-page {
    width: 100% !important;
    max-width: none !important;
    margin: 0 !important;
    padding: 0 !important;
    text-align: left !important;
}

.publication-page .publication-title {
    width: 100%;
    margin: 20px 0 32px;
    text-align: center !important;
}

.publication-page h2,
.publication-page h3,
.publication-page h4,
.publication-page p,
.publication-page ul,
.publication-page ol,
.publication-page li {
    margin-left: 0 !important;
    text-align: left !important;
}

.publication-page h2 {
    margin-top: 34px;
}

.publication-page h3 {
    margin-top: 28px;
    line-height: 1.35;
}

.publication-page p {
    line-height: 1.7;
}

.publication-page hr {
    width: 100%;
    margin: 28px 0;
}
</style>

<div class="publication-page">


During my internship, I regularly studied technical articles published by AWS and other engineering teams. In addition to completing the AWS Academy laboratories, I summarized several technical papers to deepen my understanding of cloud-native architecture, distributed systems, and modern software engineering best practices.

This section presents a collection of research notes and article summaries that I completed throughout the internship.

## List of Technical Research Articles

### Article 1 – Scaling to One Million AWS Lambda Functions: Lessons Learned from Large-Scale Serverless Architectures

[View Details](3.1-Blog1/)

**Summary:** This article explores techniques for scaling asynchronous workloads to support millions of concurrent AWS Lambda functions. By analyzing AWS Service Quotas and operational limitations, it explains how to eliminate common architectural anti-patterns, reduce bottlenecks, and build highly resilient systems.

**Applied Architecture:** Event-Driven Architecture and Workflow Orchestration.

**Core AWS Services:** AWS Lambda, Amazon SQS, AWS Step Functions, AWS SAM, and AWS CloudFormation.

---

### Article 2 – From Monolith to Multi-Account: Rebuilding AWS Organizations at Pinterest Scale

[View Details](3.2-Blog2/)

**Summary:** This article examines the challenges of migrating from a monolithic account structure to a large-scale multi-account environment. It discusses API limitations, blast-radius reduction, centralized governance, identity management, and organizational design using AWS Organizations.

**Applied Architecture:** Multi-Account Strategy and Centralized Governance.

**Core AWS Services:** AWS Organizations, AWS Control Tower, IAM Identity Center, AWS Config, and Amazon CloudTrail.

---

### Article 3 – Building Authentication and Session Management Services with Amazon Aurora DSQL

[View Details](3.3-Blog3/)

**Summary:** This article introduces a modern authentication and session management solution using Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate, and IAM Authentication. It highlights strong read-after-write consistency, secure session token management, safe credential handling, and scalable backend architecture built with managed AWS services.

**Applied Architecture:** Serverless Backend Architecture and Authentication Services.

**Core AWS Services:** Amazon Aurora DSQL, Amazon ECS Express Mode, AWS Fargate, AWS IAM, and Amazon CloudWatch.

</div>