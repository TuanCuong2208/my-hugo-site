---
title: "Worklog Week 11"
date: 2026-06-30
weight: 11
chapter: false
pre: "<b> 1.11. </b> "
---

# I. Overview Summary

Following the successful implementation of the Event-Driven Video Processing Pipeline in the previous week, the team proceeded to develop the access layer and content delivery infrastructure of the platform. The primary objective of this phase was to integrate all previously developed AWS services into a complete Video-on-Demand system that allows users to authenticate, upload videos, monitor processing status, and stream media content through a secure cloud-native architecture.

During this week, Amazon Cognito was deployed to provide user authentication and secure access control for system resources. At the same time, the web application's static resources were deployed to the Amazon S3 Frontend Bucket and distributed through Amazon CloudFront, enabling low-latency access while improving scalability and availability for end users.

In parallel, the team integrated the web interface with Amazon API Gateway to support core business functions, including user authentication, video uploads, metadata retrieval, and processing status monitoring. Video information stored in Amazon DynamoDB was synchronized with the frontend so that users could monitor the progress of each uploaded video throughout the processing lifecycle.

To further strengthen the security architecture, AWS WAF was configured in front of Amazon CloudFront to inspect incoming HTTP requests and mitigate common web-based attacks. The introduction of this additional security layer completed the multi-tier architecture proposed for the system while improving overall protection for publicly accessible resources.

By the end of the week, the authentication layer, frontend deployment, content delivery infrastructure, and backend integration had been successfully completed. Users were able to authenticate, upload videos, monitor processing progress, and stream processed media through a unified serverless platform.

# II. Weekly Strategic Objectives

Following the completion of the Event-Driven Video Processing Pipeline, the primary objective of Week 11 was to implement the user access layer and integrate every component of the platform into a complete business workflow.

The main objectives included:

- Deploy Amazon Cognito for user authentication.
- Integrate the web application with Amazon API Gateway.
- Deploy the frontend application to the Amazon S3 Frontend Bucket.
- Configure Amazon CloudFront for frontend and media content delivery.
- Implement AWS WAF to strengthen application security.
- Synchronize video metadata stored in Amazon DynamoDB with the user interface.
- Perform end-to-end integration testing across authentication, upload, processing, and playback workflows.
- Prepare the platform for system-wide testing and performance optimization.

Through these objectives, the team aimed to complete the first fully functional MVP of the Serverless Video-on-Demand Platform.

# III. Activity Log & Detailed Implementation Schedule (From 30/06/2026 to 06/07/2026)

| Time | Activity Category | Detailed Technical Tasks | Results / Deliverables |
| :--- | :--- | :--- | :--- |
| **Day 1** *(30/06)* | User Authentication | Deployed Amazon Cognito User Pool, configured user authentication, and implemented JWT token generation for authenticated users. | Successfully established the authentication infrastructure. |
| **Day 2** *(01/07)* | API Integration | Connected the web application to Amazon API Gateway to support video upload, metadata retrieval, and video management functions. | Backend APIs were successfully integrated with the frontend application. |
| **Day 3** *(02/07)* | Frontend Deployment | Deployed the web application's static resources to the Amazon S3 Frontend Bucket and configured Static Website Hosting. | The frontend application became accessible through Amazon S3. |
| **Day 4** *(03/07)* | Content Delivery | Configured Amazon CloudFront to distribute both frontend resources and processed video content stored in Amazon S3. | Improved application responsiveness and global content delivery performance. |
| **Day 5** *(04/07)* | Security Enhancement | Configured AWS WAF in front of Amazon CloudFront and implemented baseline security rules for incoming web traffic. | Completed the primary security layer for the public-facing application. |
| **Day 6** *(05/07)* | Integration Testing | Performed end-to-end testing covering user authentication, video upload, asynchronous processing, metadata synchronization, and video playback. | All system components successfully operated together according to the designed architecture. |
| **Day 7** *(06/07)* | Review & Optimization | Evaluated frontend performance, reviewed security configurations, and prepared the system for comprehensive testing. | Successfully completed the access layer and content delivery infrastructure. |

# IV. Technical Implementation & In-depth Analysis

Following the successful implementation of the Event-Driven Video Processing Pipeline, the team focused on developing the access layer that connects end users with all backend services deployed on AWS. The primary objective of this phase was to establish secure authentication, deploy the web application, configure the content delivery infrastructure, and integrate all backend APIs into a unified business workflow. This stage represents the final integration phase before comprehensive system validation and performance optimization.

The first task involved deploying Amazon Cognito as the platform's authentication service. A User Pool was configured to manage user identities, authenticate login requests, and issue JSON Web Tokens (JWT) after successful authentication. By utilizing Amazon Cognito, the team avoided implementing a custom authentication system while taking advantage of AWS-managed security features such as secure credential management, session handling, and identity verification.

After completing the authentication layer, Amazon API Gateway was configured with a Cognito Authorizer to validate JWT access tokens before granting access to protected APIs. Only authenticated users with valid tokens are permitted to perform operations such as uploading videos, retrieving metadata, or accessing video management services. Integrating Cognito directly with API Gateway simplifies backend authorization while significantly strengthening the security of the serverless application.

In parallel, the web application's static resources were deployed to the Amazon S3 Frontend Bucket using Amazon S3 Static Website Hosting. Hosting the frontend on Amazon S3 provides a highly available, scalable, and cost-effective solution that requires no server management. Once deployment was completed, Amazon CloudFront was configured to distribute the application globally through AWS Edge Locations, improving response time and reducing latency for users in different geographic regions.

Amazon CloudFront was also configured as the content delivery layer for processed media files generated by AWS Elemental MediaConvert. When users request video playback, CloudFront first attempts to retrieve cached content from the nearest Edge Location. If the requested object is unavailable in the cache, CloudFront automatically retrieves the media files from the Amazon S3 Processed Media Bucket before caching them for subsequent requests. This mechanism reduces storage access frequency, improves streaming performance, and enhances the scalability of the Video-on-Demand platform.

To strengthen application security, AWS WAF was deployed in front of Amazon CloudFront. Several baseline security rules were configured to inspect incoming HTTP requests, mitigate suspicious traffic patterns, and reduce exposure to common web application attacks. Introducing AWS WAF completed the platform's multi-layer security architecture by protecting public endpoints before requests reached CloudFront and the backend services.

After establishing the access layer, the team integrated the web application with Amazon API Gateway to complete the end-to-end business workflow. When users initiate a video upload, the application requests a Presigned URL through API Gateway. The video is then uploaded directly to the Amazon S3 Raw Upload Bucket, triggering the Event-Driven Processing Pipeline implemented during the previous week. Throughout the processing lifecycle, metadata stored in Amazon DynamoDB is continuously synchronized with the user interface. Once the processing status changes to **Completed**, users are able to stream the processed video through Amazon CloudFront.

Comprehensive integration testing was conducted after completing all system components. Test scenarios included user authentication, video uploads, asynchronous processing, metadata synchronization, and video streaming. Additional testing was performed under concurrent upload conditions to evaluate the scalability of the serverless architecture. The results confirmed that all AWS services interacted correctly and that the complete business workflow operated reliably under different operating conditions.

By the end of Week 11, the team had successfully integrated the authentication layer, frontend deployment, backend services, and content delivery infrastructure into a unified cloud-native application. Users were able to authenticate, upload videos, monitor processing progress, and stream media content through a fully functional MVP deployed entirely on AWS.

# V. Infrastructure Challenges, Troubleshooting Log & Professional Insights

One of the primary challenges encountered during this phase involved configuring authentication between Amazon Cognito and Amazon API Gateway. During the initial deployment, several API requests were rejected because JWT access tokens were not transmitted correctly within the HTTP Authorization header. After reviewing the Cognito Authorizer configuration and standardizing the token transmission process, authentication operated successfully and all protected APIs became accessible only to authorized users.

Another issue arose during the deployment of Amazon CloudFront. After updating the web application's static resources within the Amazon S3 Frontend Bucket, some users continued receiving outdated content because previous versions remained cached at CloudFront Edge Locations. To resolve this issue, CloudFront Cache Invalidation was performed after each deployment, ensuring that users consistently accessed the latest version of the application.

The implementation of AWS WAF also required careful evaluation of available security rules. The team reviewed AWS-managed rule groups and selected a baseline security configuration appropriate for the project's scope. This experience provided valuable insight into layered security strategies commonly implemented in production cloud environments while demonstrating how AWS managed security services can be integrated with minimal operational complexity.

Throughout the integration process, the team further recognized the advantages of AWS Managed Services. By relying on fully managed infrastructure instead of self-hosted servers, development efforts remained focused on business logic, system architecture, and application functionality rather than server provisioning, maintenance, and infrastructure administration.

# VI. Evaluation and Professional Reflection

Week 11 represented the successful integration of all major components into a complete Serverless Video-on-Demand Platform. Connecting authentication, backend services, storage, processing, and content delivery provided the team with valuable experience in designing and deploying a production-oriented cloud-native application using AWS managed services.

Implementing Amazon Cognito together with Amazon API Gateway strengthened the team's understanding of modern authentication mechanisms based on JSON Web Tokens (JWT) and secure API authorization within serverless environments. At the same time, deploying Amazon CloudFront and AWS WAF demonstrated how performance optimization and application security can be achieved simultaneously through AWS-native services.

The team also observed that separating authentication, processing, storage, and content delivery into independent service layers greatly simplified maintenance and future scalability. Each AWS service performs a specialized responsibility while communicating through standardized interfaces, resulting in a loosely coupled architecture that supports future feature expansion without significant architectural modifications.

Overall, every objective scheduled for Week 11 was successfully completed. The MVP now provides all essential business functionalities, including secure user authentication, direct video uploads, asynchronous processing, metadata synchronization, and video streaming through Amazon CloudFront. The platform is therefore ready for comprehensive validation, monitoring, and optimization during the final stage of the project.

# VII. Strategic Plan for the Following Week

During the final week of the internship, the team will focus on comprehensive end-to-end system validation to evaluate the reliability, performance, and operational stability of every AWS service participating in the Serverless Video-on-Demand Platform.

In parallel with functional testing, Amazon CloudWatch will be utilized to monitor logs, metrics, and workflow execution across Amazon API Gateway, AWS Lambda, AWS Step Functions, and AWS Elemental MediaConvert. The team will also review IAM configurations, evaluate AWS WAF effectiveness, optimize service configurations, and identify opportunities to improve operational efficiency while reducing infrastructure costs.

Finally, the team will complete the project's technical documentation, summarize implementation outcomes, prepare the system demonstration, and finalize presentation materials for the internship report and project evaluation. The ultimate objective is to deliver a stable MVP that fully demonstrates the feasibility of implementing a scalable Serverless Video-on-Demand Platform using AWS.