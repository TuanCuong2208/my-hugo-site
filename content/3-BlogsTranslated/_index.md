---
title: "AWS Study Group - Team Research Publications"
date: 2026-06-30
weight: 3
chapter: true
pre: "<b>3.</b>"
---

# AWS STUDY GROUP

During my internship, I regularly studied technical articles published by AWS and other engineering teams. Besides completing AWS Academy labs, I summarized several publications to better understand cloud-native architectures, distributed systems, and engineering best practices.

This page collects the research notes and article summaries completed throughout my internship.

---

## Deep-Dive Research Directory

### Blog 1 - Scaling to 1 Million AWS Lambda Functions

**Article:**
[Scaling to 1 Million AWS Lambda Functions: Hard-Earned Lessons on Massive-Scale Serverless Architecture](./blog-1/)

This article explains how AWS designs highly scalable Serverless systems using Event-Driven Architecture. It focuses on asynchronous workloads, service quotas, and workflow orchestration.

**Architecture Pattern:** Event-Driven Architecture & Workflow Orchestration

**Core AWS Services:** AWS Lambda | Amazon SQS | AWS Step Functions | AWS SAM | AWS CloudFormation

---

### Blog 2 - Pinterest Multi-Account Transformation

**Article:**
[From Monolith to Multi-Account: Pinterest's Total AWS Organization Transformation Journey at Scale](./blog-2/)

This article summarizes Pinterest's migration to a centralized multi-account environment and the governance practices used to improve scalability and security.

**Architecture Pattern:** Multi-Account Strategy & Centralized Cloud Governance

**Core AWS Services:** AWS Organizations | AWS Control Tower | AWS IAM Identity Center | AWS Config | Amazon CloudTrail

---

### Blog 3 - Authentication & Session Management

**Article:**
[Building a Modern Authentication and Session Management Service with Amazon Aurora DSQL](./blog-3/)

This article describes how AWS builds a scalable authentication platform using Aurora DSQL while maintaining secure session management and strong consistency.

**Architecture Pattern:** Serverless Backend & Authentication Service

**Core AWS Services:** Amazon Aurora DSQL | Amazon ECS Express Mode | AWS Fargate | AWS IAM | Amazon CloudWatch