---
title: "Week 9 Worklog"
date: 2026-06-16
weight: 9
chapter: false
pre: "<b>1.9. </b>"
---

## I. General Overview

The ninth week focused on completing the backend implementation of the **Serverless Video-on-Demand Platform on AWS**. During this period, the core backend services, including Amazon S3, Amazon DynamoDB, AWS Lambda, and Amazon API Gateway, were deployed and integrated into a unified serverless architecture.

Besides infrastructure deployment, the team developed backend APIs for generating Presigned URLs, storing video metadata, and retrieving video information for the web application. These components established the foundation for the video upload process and prepared the system for the automated video processing pipeline.

At the end of the week, the backend was successfully tested, allowing users to upload videos directly to Amazon S3 while metadata was stored correctly in Amazon DynamoDB. This milestone completed the backend phase of the project and prepared the environment for implementing the video processing workflow in the following week.

---

## II. Weekly Objectives

The objectives of this week were:

- Build the backend architecture using AWS serverless services.
- Create the Amazon S3 Raw Upload Bucket and Processed Media Bucket.
- Design the Amazon DynamoDB table for video metadata.
- Develop AWS Lambda functions for backend processing.
- Integrate Amazon API Gateway with AWS Lambda.
- Implement the Presigned URL upload mechanism.
- Test the video upload workflow.
- Verify metadata storage and retrieval.
- Prepare the backend for the video processing pipeline.

---

## III. Activity Log & Weekly Schedule (16/06/2026 – 22/06/2026)

| Time | Activity | Description | Result |
|------|----------|-------------|--------|
| **Day 1 (16/06)** | Backend Design | Designed the backend architecture, identified required APIs, and defined the communication flow between the web application and AWS services. | Backend architecture and API design were completed. |
| **Day 2 (17/06)** | AWS Lambda Development | Developed AWS Lambda functions responsible for generating Presigned URLs, storing metadata, and handling API requests. Configured environment variables for each function. | Lambda functions executed successfully. |
| **Day 3 (18/06)** | Amazon DynamoDB Integration | Created the **Videos** table and connected AWS Lambda to Amazon DynamoDB for storing and retrieving video metadata. | Video metadata was stored successfully. |
| **Day 4 (19/06)** | Upload Workflow | Implemented the Presigned URL upload process and tested direct uploads from the web application to Amazon S3 Raw Upload Bucket. | Videos were uploaded successfully. |
| **Day 5 (20/06)** | API Testing | Tested backend APIs for generating Presigned URLs, storing metadata, and retrieving video information under different scenarios. | All APIs returned expected results. |
| **Day 6 (21/06)** | Security Configuration | Reviewed IAM Roles, IAM Policies, API Gateway configuration, and CORS settings to ensure secure communication between AWS services. | Security configuration was completed successfully. |
| **Day 7 (22/06)** | Final Review | Reviewed backend implementation, verified system functionality, and prepared the environment for building the video processing pipeline. | Backend deployment was completed successfully. |

---

## IV. Technical Implementation & Detailed Analysis

This week's primary objective was to establish a reliable backend based entirely on AWS serverless services. Instead of managing traditional servers, the application relies on managed AWS components, allowing the system to scale automatically while reducing operational costs.

Amazon API Gateway was deployed as the entry point for all client requests. Every request from the web application is forwarded to AWS Lambda, where the corresponding business logic is executed. This architecture keeps the backend lightweight while providing flexibility for future development.

AWS Lambda was implemented to generate Presigned URLs for secure video uploads, manage metadata in Amazon DynamoDB, and process API requests. Since the video files are uploaded directly from the browser to Amazon S3, the backend only handles metadata and authentication, significantly reducing Lambda execution time and resource consumption.

Amazon DynamoDB was selected as the metadata storage service because of its high performance, scalability, and seamless integration with AWS Lambda. Each uploaded video generates a metadata record containing the video identifier, upload time, processing status, and storage location.

Throughout the implementation process, the team verified each backend component individually before performing integration tests. After all services were connected successfully, the complete upload workflow operated smoothly, demonstrating that the backend architecture met the project's functional requirements.

---

## V. Challenges, Troubleshooting & Technical Experience

Several challenges were encountered during the deployment process. The first issue involved IAM permissions, where AWS Lambda initially lacked sufficient access to Amazon S3 for generating Presigned URLs.

The team also experienced CORS configuration problems while the web application attempted to communicate with Amazon API Gateway. After reviewing API Gateway settings and updating the CORS configuration, requests from the frontend were accepted successfully.

Another issue involved environment variables inside AWS Lambda. Incorrect bucket names caused upload requests to fail during testing. Updating the configuration resolved the problem immediately.

These troubleshooting activities emphasized the importance of proper IAM configuration, consistent environment management, and systematic testing throughout the backend development process.

---

## VI. Evaluation & Professional Reflection

All objectives defined for the ninth week were successfully completed. The backend now supports secure video uploads, metadata management, and communication with the web application through REST APIs.

Working with Amazon API Gateway, AWS Lambda, Amazon DynamoDB, and Amazon S3 provided valuable practical experience in designing and implementing a serverless backend architecture.

The team also gained a deeper understanding of IAM Roles, IAM Policies, API integration, and AWS service interactions. These experiences significantly improved both technical knowledge and problem-solving skills when developing cloud-native applications.

The completed backend serves as the foundation for implementing the automated video processing pipeline in the next phase of the project.

---

## VII. Plan for Next Week

The primary objective for the following week is to implement the **Video Processing Pipeline** based on an event-driven architecture.

The planned activities include:

- Deploy Amazon SQS and Dead Letter Queue.
- Configure Amazon EventBridge notifications.
- Create EventBridge Rules for Amazon S3 events.
- Build the AWS Step Functions workflow.
- Integrate AWS Elemental MediaConvert.
- Configure EventBridge Pipes.
- Test the complete processing workflow.
- Verify processed HLS output stored in Amazon S3.
- Prepare the platform for web application integration.