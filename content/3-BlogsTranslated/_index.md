---
title: "AWS Study Group - Team Research Publications"
date: 2026-06-30
weight: 3
chapter: true
pre: "<b> 3. </b> "
---

During my internship, I regularly studied technical articles published by AWS and other engineering teams. Besides completing AWS Academy labs, I summarized several publications that helped me better understand real-world cloud architectures and modern engineering practices.

---

# Deep-Dive Research Directory

## [Scaling to 1 Million AWS Lambda Functions: Hard-Earned Lessons on Massive-Scale Serverless Architecture](./blog-1/)

This article explains how AWS designs highly scalable Serverless systems using Event-Driven Architecture. It highlights practical solutions for handling service quotas, asynchronous workloads, and large-scale workflow orchestration.

**Architecture Pattern:** Event-Driven Architecture & Workflow Orchestration

**Core AWS Services:** `AWS Lambda` | `Amazon SQS` | `AWS Step Functions` | `AWS SAM` | `AWS CloudFormation`

---

## [From Monolith to Multi-Account: Pinterest's Total AWS Organization Transformation Journey at Scale](./blog-2/)

This article presents Pinterest's migration from a single AWS account to a centralized Multi-Account environment. It focuses on governance, security, and operational management using AWS native services.

**Architecture Pattern:** Multi-Account Strategy & Centralized Cloud Governance

**Core AWS Services:** `AWS Organizations` | `AWS Control Tower` | `AWS IAM Identity Center` | `AWS Config` | `Amazon CloudTrail`

---

## [Building a Modern Authentication and Session Management Service with Amazon Aurora DSQL](./blog-3/)

This article explores how AWS builds a secure authentication platform using Amazon Aurora DSQL together with managed compute services. It also explains session management, credential protection, and backend scalability.

**Architecture Pattern:** Serverless Backend Architecture & Authentication Service

**Core AWS Services:** `Amazon Aurora DSQL` | `Amazon ECS Express Mode` | `AWS Fargate` | `AWS IAM` | `Amazon CloudWatch`