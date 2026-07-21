---
title: "Worklog Week 10"
date: 2026-06-23
weight: 10
chapter: false
pre: "<b> 1.10. </b> "
---

## I. Overview Summary

Following the completion of the backend infrastructure for direct video uploads to Amazon S3 in the previous week, the team proceeded to implement the core component of the system—the **Event-Driven Video Processing Pipeline**. The primary objective of this phase was to ensure that every uploaded video could be automatically processed, transcoded, and stored without requiring any manual intervention from system administrators.

To achieve this objective, the team designed and deployed a processing workflow based on Amazon EventBridge, Amazon SQS, Amazon EventBridge Pipes, AWS Step Functions, and AWS Elemental MediaConvert. This architecture separates event ingestion, workflow orchestration, and media processing into independent services, thereby improving scalability, fault tolerance, and maintainability while fully adhering to the serverless computing model.

Alongside the processing pipeline, the team enhanced the metadata management mechanism in Amazon DynamoDB by synchronizing the processing status of each uploaded video. Multiple processing states, including **Uploaded**, **Queued**, **Processing**, **Completed**, and **Failed**, were maintained to provide accurate tracking information for future frontend integration.

In addition, AWS Elemental MediaConvert was configured to transcode uploaded videos into the **HTTP Live Streaming (HLS)** format. The generated output files were stored in the Amazon S3 Processed Media Bucket using a structured directory organization that supports efficient content management and future delivery through Amazon CloudFront.

By the end of the week, the team successfully completed a fully automated serverless video processing pipeline. This milestone established the core business logic of the Video-on-Demand platform and laid the foundation for implementing secure content delivery and user-facing functionalities in the following development stages.

## II. Weekly Strategic Objectives

After completing the video upload functionality, the primary objective of Week 10 was to implement an asynchronous video processing architecture based entirely on AWS serverless services.

The main objectives included:

- Design and implement the Event-Driven Video Processing Pipeline.
- Configure Amazon EventBridge to receive upload events from Amazon S3.
- Deploy Amazon SQS as the message queue for processing requests.
- Configure Amazon EventBridge Pipes to transfer messages from Amazon SQS to AWS Step Functions.
- Design the video processing workflow using AWS Step Functions.
- Integrate AWS Elemental MediaConvert to transcode videos into the HLS format.
- Synchronize video processing status with Amazon DynamoDB.
- Perform end-to-end testing of the complete processing workflow from video upload to transcoding completion.

Through these objectives, the team aimed to develop a scalable and fully automated processing pipeline that complies with the proposed serverless architecture of the project.

## III. Activity Log & Detailed Implementation Schedule (From 23/06/2026 to 29/06/2026)

| Time | Activity Category | Detailed Technical Tasks | Results / Deliverables |
| :--- | :--- | :--- | :--- |
| **Day 1** *(23/06)* | Architecture Design | Analyzed the event-driven processing workflow and identified the responsibilities of Amazon EventBridge, Amazon SQS, Amazon EventBridge Pipes, AWS Step Functions, and AWS Elemental MediaConvert. | Completed the architectural design of the Video Processing Pipeline. |
| **Day 2** *(24/06)* | Event Layer Deployment | Configured Amazon EventBridge to capture Object Created events from the Amazon S3 Raw Upload Bucket and forward them to Amazon SQS. | Upload events were successfully captured and delivered to the processing queue. |
| **Day 3** *(25/06)* | Workflow Orchestration | Configured Amazon EventBridge Pipes to retrieve messages from Amazon SQS and trigger AWS Step Functions for workflow execution. | Successfully established the asynchronous orchestration workflow. |
| **Day 4** *(26/06)* | Video Transcoding | Integrated AWS Elemental MediaConvert into the Step Functions workflow and configured HLS transcoding profiles. | Uploaded videos were successfully transcoded and stored in the Amazon S3 Processed Media Bucket. |
| **Day 5** *(27/06)* | Metadata Management | Updated video processing states in Amazon DynamoDB, including Queued, Processing, Completed, and Failed. | Video metadata accurately reflected the processing lifecycle. |
| **Day 6** *(28/06)* | Pipeline Testing | Executed multiple upload scenarios while monitoring Amazon EventBridge, Amazon SQS, AWS Step Functions, and MediaConvert throughout the processing workflow. | The processing pipeline operated reliably under various testing scenarios. |
| **Day 7** *(29/06)* | Review & Optimization | Reviewed the entire processing architecture, optimized workflow execution, evaluated scalability, and prepared for the content delivery layer. | Successfully completed the automated serverless Video Processing Pipeline. |

## IV. Technical Implementation & In-depth Analysis

Following the successful implementation of the direct video upload mechanism in the previous week, the team focused on building the core processing layer of the platform based on an event-driven serverless architecture. The objective of this phase was to develop an automated workflow capable of receiving upload events, orchestrating media processing tasks, and generating streaming-ready video files without requiring manual intervention. To accomplish this objective, the processing pipeline was designed by combining Amazon EventBridge, Amazon SQS, Amazon EventBridge Pipes, AWS Step Functions, and AWS Elemental MediaConvert.

The first component implemented during this phase was Amazon EventBridge. Whenever a user successfully uploads a video to the Amazon S3 Raw Upload Bucket, an **Object Created** event is automatically generated and captured by EventBridge. Instead of directly invoking downstream processing services, EventBridge acts as the event routing layer, decoupling event generation from business logic execution. This architectural approach improves flexibility and allows additional processing services to be integrated in the future without modifying the upload workflow.

To increase system reliability and support asynchronous processing, Amazon SQS was deployed as an intermediate message queue. Every upload event is converted into a message and stored inside the queue before being processed. Using Amazon SQS prevents temporary traffic spikes from overwhelming downstream services while ensuring that processing requests are retained until they are successfully consumed. This buffering mechanism significantly improves the scalability and fault tolerance of the overall system.

Once messages become available in the queue, Amazon EventBridge Pipes continuously retrieves them and forwards the corresponding payload to AWS Step Functions. By utilizing EventBridge Pipes, the team eliminated the need to develop custom polling services or additional middleware for integrating Amazon SQS with Step Functions. This native AWS integration reduced development complexity while simplifying the management of the processing workflow.

AWS Step Functions was then configured as the orchestration engine responsible for managing the complete video processing lifecycle. The workflow was implemented as a State Machine consisting of multiple sequential processing stages, including input validation, workflow initialization, media transcoding, metadata synchronization, and completion handling. Using Step Functions provides clear workflow visualization, centralized execution management, automatic retry capabilities, and simplified error handling throughout the processing pipeline.

During the transcoding stage, AWS Elemental MediaConvert was integrated into the workflow to convert uploaded videos into the **HTTP Live Streaming (HLS)** format. Input videos were retrieved from the Amazon S3 Raw Upload Bucket, while the generated HLS playlist (.m3u8) and transport stream segments (.ts) were stored in the Amazon S3 Processed Media Bucket. The output directory structure was organized according to individual video identifiers, improving content management and simplifying future integration with the content delivery layer.

Simultaneously, the processing workflow continuously synchronized video metadata with Amazon DynamoDB. Each video record was updated throughout its lifecycle using predefined processing states, including **Uploaded**, **Queued**, **Processing**, **Completed**, and **Failed**. Maintaining processing status within DynamoDB allows other system components to retrieve real-time progress information without directly communicating with MediaConvert or Step Functions, thereby reducing service dependencies.

After implementing each processing component, comprehensive end-to-end testing was conducted using multiple upload scenarios involving different video formats and file sizes. The team monitored event routing, queue processing, workflow execution, transcoding operations, and metadata synchronization throughout the entire pipeline. Testing results demonstrated that all AWS services cooperated correctly and that the complete serverless workflow operated consistently under various processing conditions.

By the conclusion of Week 10, the team had successfully established a fully automated event-driven processing pipeline. From the moment a user uploads a video until the transcoded output is generated and metadata is updated, every stage of the workflow is executed automatically through managed AWS services. This achievement represents one of the most critical technical milestones of the project and provides the foundation for implementing secure content delivery and frontend integration during the following development phase.

## V. Infrastructure Challenges, Troubleshooting Log & Professional Insights

During the deployment of the processing pipeline, one of the first challenges involved configuring the permissions between AWS Step Functions and AWS Elemental MediaConvert. Initially, several workflow executions failed because the assigned IAM Role did not have sufficient permissions to access Amazon S3 resources and initiate MediaConvert jobs. After reviewing the IAM policies and applying the Principle of Least Privilege, the required permissions were correctly assigned, allowing the workflow to execute successfully while maintaining system security.

Another issue emerged during the integration of Amazon EventBridge and Amazon SQS. Early testing revealed that certain upload events were not forwarded to the message queue because the EventBridge Event Pattern did not accurately match Amazon S3 Object Created events. After refining the event filtering rules and validating multiple upload scenarios, the team ensured that every uploaded video consistently entered the asynchronous processing pipeline.

While implementing AWS Step Functions, the team recognized the advantages of dividing the processing workflow into multiple independent states. Instead of executing all processing tasks within a single service, each state performs a dedicated responsibility, making execution progress easier to monitor and simplifying troubleshooting whenever failures occur. This modular workflow design also improves maintainability and supports future enhancements without affecting existing processing stages.

The implementation further demonstrated the practical value of Amazon SQS within distributed systems. By introducing an intermediate message queue, the processing workflow remains stable even during periods of increased upload activity. This architecture provides sufficient flexibility for future system expansion while minimizing the risk of service overload or processing interruptions.

## VI. Evaluation and Professional Reflection

Week 10 significantly improved the team's understanding of building asynchronous cloud-native applications using AWS managed services. Compared with the previous development phases, this stage focused less on implementing individual backend functions and more on designing a coordinated workflow capable of orchestrating multiple cloud services within a single processing pipeline.

The implementation also strengthened the team's practical knowledge of Event-Driven Architecture and Workflow Orchestration. Separating event routing, message queuing, workflow coordination, and media transcoding into independent services resulted in a more scalable, maintainable, and fault-tolerant system architecture that aligns with modern cloud application design principles.

In addition, deploying AWS Elemental MediaConvert provided valuable experience in cloud-based multimedia processing. The service proved highly suitable for Video-on-Demand platforms due to its support for multiple media formats, automated transcoding workflows, and seamless integration with other AWS storage and orchestration services.

Overall, every objective planned for Week 10 was successfully achieved. The automated video processing pipeline now operates reliably within the AWS cloud environment and establishes the technical foundation required for secure content delivery, frontend integration, and complete system deployment during the remaining stages of the project.

## VII. Strategic Plan for the Following Week

During the following week, the team will focus on implementing the user access layer of the platform by integrating Amazon Cognito, Amazon CloudFront, and the Amazon S3 Frontend Bucket. In addition, the web application will be connected to Amazon API Gateway to support user authentication, video uploads, metadata retrieval, and video playback.

Alongside frontend integration, comprehensive end-to-end testing will be performed across the complete business workflow, including user authentication, video upload, asynchronous processing, metadata synchronization, and content delivery. The objective of the next development phase is to complete the first fully functional MVP of the Video-on-Demand platform while preparing the system for performance optimization, monitoring, and final deployment.