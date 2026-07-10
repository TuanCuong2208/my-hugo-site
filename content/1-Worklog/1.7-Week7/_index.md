---
title: "Worklog Week 7"
date: 2026-06-02
weight: 7
chapter: false
pre: "<b> 1.7. </b> "
---

### I. Executive Summary

Week 7 marked an important transition in the internship journey as the team completed the AWS Academy learning phase and began preparing for the implementation of the internship project. Instead of continuing with individual AWS laboratory exercises, the team shifted its focus toward consolidating the knowledge acquired throughout the training program and applying it to a real-world cloud solution.

During this week, the team analyzed the business requirements of the proposed system, evaluated different architectural approaches available on AWS, and assessed how each AWS service could contribute to the overall solution. After several discussions and technical evaluations, the team decided to adopt a **Serverless Architecture** combined with an **Event-Driven Architecture** to maximize scalability, minimize operational overhead, and optimize infrastructure costs.

In parallel with the research process, the team produced the first draft of the overall system architecture. The proposed design identified the responsibilities of core AWS services, including Amazon S3, Amazon API Gateway, AWS Lambda, Amazon Cognito, Amazon DynamoDB, Amazon CloudFront, Amazon SQS, and AWS Elemental MediaConvert throughout the video processing workflow. This initial architecture serves as the technical foundation for implementing individual modules in the upcoming development phases.

By the end of the week, the team completed the first version of the system architecture, established an implementation roadmap for future milestones, and prepared the technical documentation required for the development stage.

### II. Strategic Objectives

Following the completion of the AWS Academy curriculum, the primary objective of Week 7 was to transition from the learning phase to the solution design phase for the internship project. The team focused on building a solid technical foundation before starting the implementation of the application.

The strategic objectives for this week included:

- Consolidate and organize the AWS knowledge acquired throughout the AWS Academy program to support system architecture design.
- Analyze the business requirements of the Video-on-Demand platform and identify its core functional modules.
- Evaluate multiple cloud architecture patterns and determine the suitability of a Serverless architecture for the project.
- Select the most appropriate AWS services for authentication, business logic, data storage, video processing, and content delivery.
- Develop the first draft of the overall system architecture (Architecture Draft V1) as the baseline for future implementation.
- Define a development roadmap and organize implementation phases to ensure project scalability and maintainability.

Through these objectives, the team aimed to establish a feasible architectural foundation while preparing for the implementation of individual system components in the following weeks.

### III. Activity Log & Detailed Work Allocation (From 02/06/2026 to 08/06/2026)

| Time | Activity Category | Detailed Technical Tasks | Achievements / Evidence |
| :--- | :--- | :--- | :--- |
| **Day 1** *(02/06)* | AWS Knowledge Consolidation | Reviewed and organized the knowledge acquired throughout the AWS Academy program, covering Compute, Storage, Database, Networking, Security, and Serverless services in preparation for the internship project. | Completed a consolidated reference document of AWS core services and architectural best practices. |
| **Day 2** *(03/06)* | Business Requirement Analysis | Discussed the functional requirements of the Video-on-Demand platform, including user management, video upload, video processing, and online video streaming. | Defined the project scope and established the overall business workflow of the system. |
| **Day 3** *(04/06)* | Solution Research | Evaluated multiple AWS architecture patterns and assessed the applicability of Serverless and Event-Driven Architecture for large-scale video processing. | Selected a Serverless-based architecture as the primary implementation approach. |
| **Day 4** *(05/06)* | Overall Architecture Design | Designed the initial system architecture by identifying the relationships between the Frontend, Backend, Data Layer, and Video Processing Pipeline. | Completed the first draft of the system architecture. |
| **Day 5** *(06/06)* | AWS Service Selection | Evaluated and selected appropriate AWS services, including Amazon S3, Amazon API Gateway, AWS Lambda, Amazon Cognito, Amazon DynamoDB, Amazon CloudFront, Amazon SQS, and AWS Elemental MediaConvert for different system components. | Finalized the initial AWS service stack for the project. |
| **Day 6** *(07/06)* | Development Roadmap Planning | Divided the project into functional modules and established an implementation roadmap for subsequent development phases. | Completed the initial project development roadmap. |
| **Day 7** *(08/06)* | Project Preparation | Reviewed the proposed architecture, consolidated research materials, and prepared the technical environment for the upcoming implementation stage. | Completed the preliminary technical documentation and prepared for system development. |

### IV. In-depth Technical Execution & Analysis

After completing the AWS Academy training program, the team entered a new phase that shifted the primary focus from learning individual AWS services to designing an integrated cloud solution for the internship project. Rather than implementing standalone laboratory exercises, this week was dedicated to understanding the business problem, evaluating architectural approaches, and proposing a practical cloud architecture capable of supporting future development.

Following several technical discussions, the team agreed to develop a **Mini Video-on-Demand Platform using AWS Serverless**. The proposed system is designed to allow administrators to upload video content, automatically process and transcode media into multiple resolutions, and distribute the final content efficiently through a Content Delivery Network (CDN). This project was selected because it leverages a wide range of AWS managed services while demonstrating the advantages of a modern Serverless and Event-Driven architecture.

At this stage, the objective was not to implement individual components but to establish an architectural blueprint that defines the responsibilities of each service and the interaction between different layers of the system.

<img src="/images/week7/1.png" alt="Initial Serverless Video-on-Demand Architecture" style="max-width:100%; height:auto;" />

The proposed architecture is divided into several logical layers to improve modularity, scalability, and maintainability.

#### 1. Frontend Layer

The frontend application is planned to be developed using **React/Next.js**, providing a responsive and modern user interface for both administrators and viewers.

Instead of deploying a traditional web server, the frontend will be hosted as a **Static Website** on **Amazon S3**, with **Amazon CloudFront** serving as the global Content Delivery Network. This deployment model reduces infrastructure management while improving page loading performance through edge caching.

Separating the frontend from backend services also aligns well with the overall Serverless architecture and simplifies future maintenance.

#### 2. API & Authentication Layer

The communication between clients and backend services will be handled by **Amazon API Gateway**, which acts as the centralized entry point for all RESTful APIs.

For authentication and user management, the team selected **Amazon Cognito**. By utilizing Cognito User Pools and JWT-based authentication, the system can securely manage user identities without implementing a custom authentication solution.

During this stage, the team focused on defining Cognito's role within the architecture. Detailed configuration of User Pools, Authorization Flows, and Identity Providers will be performed during the implementation phase.

#### 3. Business Logic Layer

Business logic will be implemented entirely using **AWS Lambda**.

Lambda provides automatic scaling, eliminates server management, and follows a pay-per-use pricing model, making it well suited for workloads with unpredictable traffic patterns such as video streaming platforms.

Several Lambda functions have been identified in the initial design, including:

- API request processing
- Presigned URL generation
- Video status management
- Event-driven processing tasks

Each function is designed to remain independent and communicate through API Gateway or AWS event services, minimizing coupling between system components.

#### 4. Data Layer

The system will utilize **Amazon DynamoDB** to store video metadata and processing information.

The initial data model is expected to include:

- Video ID
- Video title
- Processing status
- Storage location
- Upload timestamp
- Category
- Uploader information

DynamoDB was selected because of its scalability, high performance, and seamless integration with serverless workloads.

The team also plans to introduce Global Secondary Indexes (GSIs) to support efficient querying based on processing status and video categories. The detailed schema design will be finalized in the following development phase.

#### 5. Video Processing Pipeline

The Video Processing Pipeline represents the core component of the proposed architecture.

To improve scalability and user experience, the team intends to implement the entire workflow using an **Event-Driven Architecture**.

The proposed processing flow consists of the following steps:

1. An administrator requests to upload a video.
2. The backend generates a Presigned URL.
3. The video is uploaded directly to the Amazon S3 Raw Bucket.
4. An upload event is generated automatically.
5. Amazon SQS receives the processing request.
6. AWS Lambda submits a transcoding job to AWS Elemental MediaConvert.
7. MediaConvert generates multiple streaming resolutions.
8. Processed outputs are stored in the Processed Bucket.
9. Amazon EventBridge detects job completion.
10. AWS Lambda updates the processing status in DynamoDB.

This asynchronous architecture prevents long-running API requests, improves fault tolerance, and enables each component to scale independently according to workload demands.

#### 6. Content Delivery

Once transcoding is completed, processed videos will be delivered through **Amazon CloudFront**.

CloudFront is expected to provide several important benefits:

- Lower content delivery latency
- Global edge caching
- Reduced workload on Amazon S3
- Improved streaming performance

The architecture is also designed to support **HTTP Live Streaming (HLS)**, allowing clients to automatically switch video quality based on network conditions.

#### 7. Security and Observability Considerations

Besides the primary functional components, the proposed architecture also incorporates several AWS services responsible for security, monitoring, and operational governance.

The initial design includes:

- **AWS IAM** for role-based access control following the Principle of Least Privilege.
- **AWS KMS** for data encryption.
- **Amazon CloudWatch** for monitoring metrics and application logs.
- **AWS CloudTrail** for auditing API activities.
- **AWS WAF** for protecting publicly exposed endpoints.

At this stage, these services have only been identified as architectural components. Their detailed configuration and optimization will be carried out during future implementation phases.

### Technical Evaluation

The primary outcome of this week was the completion of the first architectural proposal rather than functional implementation. Although no application modules have been developed yet, defining the interaction between AWS services and establishing a clear architectural direction provides a strong technical foundation for subsequent development.

The current architecture should be considered an initial design draft. As implementation progresses and feedback is received from the project supervisor, the team expects to refine the architecture, improve service integration, and optimize both operational cost and system performance before reaching the final production-ready design.