---
title: "Proposal"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Introduction

With the rapid growth of online learning, corporate training, and digital content sharing, Video-on-Demand (VoD) platforms have become increasingly important in delivering multimedia content efficiently and reliably. However, building a traditional VoD system often requires high-performance servers to process, store, and stream video content to multiple users simultaneously, resulting in significant infrastructure and operational costs.

To address these challenges, this project proposes the development of a **Serverless Video-on-Demand Platform on AWS**, leveraging Amazon Web Services' fully managed serverless services. The platform automates the entire workflow, including video upload, processing, storage, and streaming, while minimizing infrastructure management.

The proposed solution aims to reduce operational complexity, optimize resource utilization, and provide a scalable and highly available architecture capable of handling future growth in both video content and user traffic.

---

# Problem Statement and Proposed Solution

## Problem Statement

In many conventional systems, video processing tasks are performed directly on the application server. As the number of uploaded videos increases, the server must simultaneously handle file uploads, video transcoding, storage management, and content delivery. This approach consumes significant computing resources, degrades overall system performance, and increases infrastructure costs.

Furthermore, scaling a traditional architecture often requires deploying additional servers or upgrading hardware resources, making the system more expensive and difficult to maintain.

## Proposed Solution

This project proposes a Serverless Video-on-Demand platform built on Amazon Web Services. Uploaded videos are stored in Amazon S3, where an upload event automatically triggers a processing pipeline using Amazon EventBridge, Amazon SQS, and AWS Step Functions. AWS Elemental MediaConvert transcodes videos into streaming-compatible formats, while Amazon CloudFront distributes video content with low latency.

The backend is implemented using Amazon API Gateway and AWS Lambda, with Amazon DynamoDB storing video metadata. User authentication is handled through Amazon Cognito before accessing the platform.

By adopting an Event-Driven Architecture, computing resources are only consumed when processing requests occur, significantly reducing operational costs while improving scalability and system efficiency.

---

# Proposed Architecture

The system architecture is designed using fully managed serverless services provided by Amazon Web Services. Each component is responsible for a specific task and communicates through APIs or event-driven interactions.

<img src="/images/2-Proposal/1.png" alt="Initial Serverless Video-on-Demand Architecture" style="max-width:100%; height:auto;" />

The overall workflow is described as follows:

1. Users authenticate through Amazon Cognito.
2. The frontend sends requests to Amazon API Gateway.
3. AWS Lambda processes requests and generates a Pre-signed URL.
4. Videos are uploaded directly to the Amazon S3 Raw Upload Bucket.
5. Amazon EventBridge detects the upload event and forwards it to Amazon SQS.
6. EventBridge Pipes trigger AWS Step Functions.
7. AWS Step Functions orchestrate the video processing workflow using AWS Elemental MediaConvert.
8. Processed videos are stored in the Amazon S3 Processed Media Bucket.
9. Amazon DynamoDB updates the processing status and video metadata.
10. Users access video content through Amazon CloudFront.

The primary AWS services used in the proposed architecture include Amazon Cognito, Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon S3, Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, AWS Elemental MediaConvert, Amazon CloudFront, and Amazon CloudWatch.

---

# Implementation Plan

The project is divided into several development phases to ensure systematic implementation, testing, and deployment. Each phase focuses on a specific set of functionalities, making project management and progress evaluation more effective.

| Phase | Activities |
|---------|------------|
| Phase 1 | Requirement analysis and AWS service evaluation |
| Phase 2 | System architecture and database design |
| Phase 3 | Frontend and Backend API development |
| Phase 4 | Video upload workflow and MediaConvert integration |
| Phase 5 | CloudFront integration, system testing, and final deployment |

Each development phase includes functional testing to identify and resolve issues before proceeding to the next stage. Once all features are completed, the application will be deployed on AWS for performance evaluation and project demonstration.

---

# Estimated Cost

Since the platform is built using a Serverless architecture, most AWS services follow a **Pay-as-you-go** pricing model, meaning charges are incurred only when resources are actually used. Considering the limited scope of this project, the expected deployment cost remains relatively low.

| AWS Service | Purpose |
|--------------|---------|
| Amazon S3 | Video storage |
| Amazon CloudFront | Content delivery |
| Amazon API Gateway | REST API |
| AWS Lambda | Backend processing |
| Amazon DynamoDB | Video metadata storage |
| Amazon Cognito | User authentication |
| Amazon EventBridge | Event routing |
| Amazon SQS | Message queue |
| AWS Step Functions | Workflow orchestration |
| AWS Elemental MediaConvert | Video transcoding |
| Amazon CloudWatch | Monitoring and logging |

Assuming approximately 10–20 uploaded videos and a limited number of users during testing, the estimated deployment cost ranges between **USD 5 and USD 10**. After the project demonstration and evaluation, all AWS resources will be removed to prevent unnecessary charges.

---

# Expected Outcomes

Upon completion, the project is expected to achieve the following objectives:

- Successfully develop a Serverless Video-on-Demand platform on AWS.
- Automate the complete workflow of video upload, processing, and streaming.
- Support HLS video transcoding for adaptive streaming.
- Deliver video content efficiently through Amazon CloudFront.
- Manage video metadata and processing status using Amazon DynamoDB.
- Provide a scalable, highly available, and cost-effective solution through fully managed AWS services.

In addition to implementing the core functionalities of a Video-on-Demand platform, this project enables the development team to gain practical experience with Serverless Architecture, Event-Driven Design, and the integration of multiple AWS services into a unified cloud solution. The proposed architecture also provides a solid foundation for future enhancements, such as user management, viewing statistics, video search, and AI-powered features using AWS services.

---

# Conclusion

The **Serverless Video-on-Demand Platform on AWS** demonstrates how AWS serverless technologies can be utilized to build a scalable, cost-efficient, and highly available video streaming platform while minimizing infrastructure management.

By integrating Amazon S3, AWS Lambda, Amazon API Gateway, Amazon DynamoDB, AWS Elemental MediaConvert, Amazon CloudFront, Amazon EventBridge, Amazon SQS, and AWS Step Functions, the system automates the complete video processing pipeline from upload to content delivery.

This proposal serves as the foundation for the implementation, testing, deployment, and future enhancement of the project throughout the development lifecycle.