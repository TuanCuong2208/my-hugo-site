---
title: "Worklog Week 7"
date: 2026-06-02
weight: 7
chapter: false
pre: "<b>1.7. </b>"
---

### I. Executive Summary

Week 7 marked an important transition during the internship as the team completed the AWS Academy training program and officially entered the research and solution design phase of the internship project. Instead of continuing with individual laboratory exercises, the team focused on consolidating the knowledge acquired throughout the training program and applying it to a practical cloud-based system.

After several discussions and technical evaluations, the team selected **Serverless Video-on-Demand Platform on AWS** as the internship project. The objective of the platform is to allow users to authenticate, upload videos, monitor processing status, and stream processed videos through a fully managed serverless architecture on AWS.

During this week, the team analyzed the business requirements of the platform and evaluated several architectural approaches suitable for cloud-native applications. Considering the characteristics of video processing workloads, a combination of **Serverless Architecture** and **Event-Driven Architecture** was identified as the most appropriate solution because of its scalability, cost efficiency, and reduced operational overhead.

The team also identified the AWS services required for the project, including Amazon S3, Amazon CloudFront, Amazon Cognito, Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, AWS Elemental MediaConvert, and Amazon CloudWatch. Each service was analyzed according to its responsibility within the overall system architecture.

In addition, the project was divided into several logical components, including the Web Application, Backend API, Metadata Storage, and Video Processing Pipeline. This modular design simplifies future implementation and improves maintainability as the project evolves.

By the end of the week, the team completed the requirement analysis, finalized the MVP scope, established the overall architectural direction, and prepared the development roadmap for the implementation phase.

---

### II. Strategic Objectives

Following the completion of the AWS Academy program, the primary objective of Week 7 was to transition from theoretical learning to the architectural planning stage of the internship project. Rather than implementing cloud resources immediately, the team focused on establishing a solid technical foundation for future development.

The main objectives of the week were:

- Consolidate the knowledge acquired from AWS Academy.
- Analyze the business requirements of the Video-on-Demand platform.
- Define the functional scope of the MVP.
- Evaluate suitable cloud architecture patterns on AWS.
- Compare traditional and serverless deployment models.
- Identify appropriate AWS services for each system component.
- Design the overall asynchronous video processing workflow.
- Divide the project into independent functional modules.
- Prepare the implementation roadmap for subsequent development phases.
- Organize technical documents required for the implementation stage.

These objectives provide a clear architectural direction and reduce potential design changes during future development.

---

### III. Activity Log & Weekly Schedule

| Date | Activity | Description | Outcome |
| :--- | :--- | :--- | :--- |
| **Day 1** *(02/06)* | AWS Knowledge Review | Reviewed AWS Academy topics covering Compute, Storage, Database, Networking, Security, and Serverless services. | Completed a consolidated technical reference for the project. |
| **Day 2** *(03/06)* | Business Requirement Analysis | Identified the system objectives and major features, including authentication, video upload, metadata management, processing status, and video streaming. | Defined the functional scope of the MVP. |
| **Day 3** *(04/06)* | Architecture Research | Studied multiple AWS deployment models and evaluated Serverless and Event-Driven Architecture for the project. | Selected Serverless Architecture as the primary solution. |
| **Day 4** *(05/06)* | AWS Service Selection | Evaluated Amazon S3, CloudFront, Cognito, API Gateway, Lambda, DynamoDB, EventBridge, SQS, EventBridge Pipes, Step Functions, and MediaConvert. | Finalized the AWS services required for the project. |
| **Day 5** *(06/06)* | Workflow Design | Designed the overall workflow from video upload, processing, metadata update, and video delivery. | Completed the initial business workflow of the platform. |
| **Day 6** *(07/06)* | Project Planning | Divided the project into Web Application, Backend API, Metadata Storage, and Video Processing Pipeline modules. | Completed the implementation roadmap for future development. |
| **Day 7** *(08/06)* | Weekly Review | Reviewed all technical documents, finalized the architectural direction, and prepared for the implementation phase. | Completed the planning stage and prepared for AWS infrastructure deployment. |

### IV. Technical Implementation & Detailed Analysis

After completing the AWS Academy training program, the team entered the research and solution design phase of the internship project. Instead of immediately deploying AWS services, the primary focus during this week was to analyze business requirements, evaluate architectural approaches, and define a suitable technical direction for the proposed Video-on-Demand platform.

Following several discussions and technical evaluations, the team selected a **Serverless Architecture** combined with an **Event-Driven Architecture** as the foundation of the system. This approach provides automatic scalability, reduces infrastructure management effort, and is particularly suitable for video processing workloads, which usually require long execution times and asynchronous operations.

For the presentation layer, the team planned to deploy the web application as a static website hosted on **Amazon S3** and distributed through **Amazon CloudFront**. This architecture separates the frontend from the backend while improving content delivery performance and simplifying deployment.

The backend services were designed around **Amazon API Gateway** and **AWS Lambda**. API Gateway serves as the entry point for client requests, while Lambda functions handle application logic such as generating upload URLs, managing video metadata, and responding to user requests. This design eliminates the need for server management and allows the application to scale automatically according to demand.

For data storage, the team selected **Amazon DynamoDB** to manage video metadata, including video identifiers, titles, processing status, storage locations, upload timestamps, and uploader information. DynamoDB was chosen because of its high scalability and seamless integration with serverless applications.

The most important component of the platform is the **Video Processing Pipeline**. After evaluating different processing models, the team decided to adopt an event-driven workflow. Once a video is uploaded to the **Amazon S3 Raw Upload Bucket** through a Presigned URL, an event will trigger the processing pipeline automatically.

The proposed pipeline consists of **Amazon EventBridge**, **Amazon SQS**, **EventBridge Pipes**, **AWS Step Functions**, and **AWS Elemental MediaConvert**. After the transcoding process is completed, the processed video will be stored in the **Amazon S3 Processed Media Bucket**, while the corresponding metadata in **Amazon DynamoDB** will be updated to reflect the latest processing status.

In addition to these core services, the team also planned to integrate **Amazon Cognito** for user authentication and **Amazon CloudWatch** for monitoring application logs and system performance. Although these services were not deployed during this week, their responsibilities within the overall architecture were clearly identified.

---

### V. Infrastructure Challenges, Problem Analysis & Technical Observations

Although no production infrastructure was deployed during Week 7, the team identified several technical challenges that needed to be addressed before the implementation phase.

The first challenge involved selecting an appropriate architecture for handling video processing tasks. Since video transcoding is computationally intensive and time-consuming, a synchronous processing model would increase response latency and potentially exceed the execution limits of serverless services. Therefore, the team adopted an asynchronous processing approach based on event-driven communication.

Another important consideration was uploading large video files. Instead of transferring video data through the backend, the team decided to generate **Presigned URLs**, allowing clients to upload videos directly to Amazon S3. This approach significantly reduces backend workload while improving upload performance.

The synchronization between **Amazon S3** and **Amazon DynamoDB** was also recognized as an important design consideration. To maintain consistency across services, the team planned to use a unique **Video ID** as the primary identifier linking metadata records with the corresponding objects stored in Amazon S3.

In addition, security and access management were considered early in the design process. The team agreed that each AWS service should receive only the permissions required for its specific responsibilities by following the **Principle of Least Privilege**.

---

### VI. Professional Reflection

Week 7 served as the transition from technical training to practical system design. Although no application modules were implemented, this stage played a critical role in establishing a solid technical foundation for the project.

Throughout the research process, the team gained a deeper understanding of how AWS services such as Amazon S3, Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon EventBridge, Amazon SQS, AWS Step Functions, and AWS Elemental MediaConvert can work together within a serverless environment to support a complete Video-on-Demand platform.

Besides improving technical knowledge, the team also strengthened essential software engineering skills, including requirement analysis, architectural evaluation, solution planning, and project organization. These experiences will contribute significantly to the successful implementation of the system in the following weeks.

---

### VII. Strategic Plan for the Following Week

After completing the research and architectural design phase, the team will begin preparing the implementation environment for the project.

The main objectives for the following week include:

- Finalize the detailed technical design.
- Prepare the AWS development environment.
- Initialize the project repository and directory structure.
- Configure Amazon S3 buckets and Amazon DynamoDB.
- Develop the first backend APIs using Amazon API Gateway and AWS Lambda.
- Prepare the foundation of the Video Processing Pipeline.
- Begin developing the web application for system testing.

The primary goal of the following week is to establish the initial cloud infrastructure and implement the core components required for the **Serverless Video-on-Demand Platform on AWS**, providing a solid foundation for subsequent development stages.