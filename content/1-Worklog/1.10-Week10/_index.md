---
title: "Week 10 Worklog"
date: 2026-06-23
weight: 10
chapter: false
pre: "<b>1.10. </b>"
---

## I. General Overview

After completing the backend implementation, the tenth week focused on building the **Video Processing Pipeline** based on an event-driven architecture. The objective was to automate the entire video processing workflow, allowing uploaded videos to be transcoded without manual intervention.

To achieve this goal, the team integrated several AWS services, including Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, and AWS Elemental MediaConvert. Each service was configured to perform a dedicated task within the processing workflow while maintaining loose coupling between system components.

Multiple integration tests were conducted throughout the week to verify that newly uploaded videos automatically triggered the processing pipeline and generated HLS output files. The successful completion of this stage transformed the system from a simple storage platform into a functional Video-on-Demand solution capable of processing streaming content.

---

## II. Weekly Objectives

The objectives for this week included:

- Build an event-driven video processing pipeline.
- Create Amazon SQS and Dead Letter Queue.
- Enable Amazon EventBridge notifications.
- Configure EventBridge Rules.
- Build the AWS Step Functions workflow.
- Integrate AWS Elemental MediaConvert.
- Configure EventBridge Pipes.
- Verify automatic workflow execution.
- Test video transcoding.
- Validate processed HLS output.

---

## III. Activity Log & Weekly Schedule (23/06/2026 – 29/06/2026)

| Time | Activity | Description | Result |
|------|----------|-------------|--------|
| **Day 1 (23/06)** | Pipeline Design | Designed the event-driven processing workflow and defined the interaction between Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, and AWS Elemental MediaConvert. | Pipeline architecture completed. |
| **Day 2 (24/06)** | Amazon SQS Deployment | Created the Processing Queue and Dead Letter Queue. Configured retry policies and verified queue functionality. | Amazon SQS operated successfully. |
| **Day 3 (25/06)** | Amazon EventBridge | Enabled EventBridge notifications for the Raw Upload Bucket and configured EventBridge Rules to forward upload events to Amazon SQS. | Upload events were delivered successfully. |
| **Day 4 (26/06)** | AWS Step Functions | Built the workflow using AWS Step Functions and integrated AWS Elemental MediaConvert into the processing sequence. | Workflow deployment completed successfully. |
| **Day 5 (27/06)** | MediaConvert Configuration | Configured MediaConvert input, output, IAM Role, and transcoding settings for HLS generation. | MediaConvert jobs executed correctly. |
| **Day 6 (28/06)** | EventBridge Pipes | Connected Amazon SQS with AWS Step Functions through EventBridge Pipes and tested automatic workflow triggering. | Automatic execution was verified successfully. |
| **Day 7 (29/06)** | System Testing | Uploaded multiple videos with different sizes and monitored Step Functions executions, MediaConvert jobs, and generated output files. | The processing pipeline operated successfully. |

---

## IV. Technical Implementation & Detailed Analysis

The primary task during this week was implementing a fully automated video processing workflow based on AWS event-driven services. Rather than allowing the backend to handle long-running processing tasks, the team distributed responsibilities across multiple AWS managed services to improve scalability and system reliability.

Whenever a new video is uploaded to the Amazon S3 Raw Upload Bucket, Amazon EventBridge immediately captures the Object Created event. Instead of invoking the processing workflow directly, the event is forwarded to Amazon SQS. This intermediate queue allows the system to process requests asynchronously and prevents temporary failures from interrupting the workflow.

Amazon SQS also improves fault tolerance by buffering incoming requests when multiple uploads occur simultaneously. In addition, a Dead Letter Queue was configured to store messages that could not be processed successfully after multiple retry attempts, simplifying troubleshooting and monitoring.

EventBridge Pipes was introduced to automatically transfer messages from Amazon SQS to AWS Step Functions without requiring an additional AWS Lambda function. This approach simplifies the architecture while reducing operational complexity.

AWS Step Functions coordinates the complete video processing workflow. Each execution creates an AWS Elemental MediaConvert job responsible for transcoding uploaded videos into HLS format. Because the workflow is centrally managed, future processing steps such as thumbnail generation, AI analysis, or notification services can be added without redesigning the architecture.

AWS Elemental MediaConvert performs the actual transcoding process. The output consists of HLS playlists and media segments, which are stored in the Amazon S3 Processed Media Bucket. These files are later distributed through Amazon CloudFront for video streaming.

The completed pipeline successfully demonstrated the advantages of event-driven serverless architecture, including automatic scalability, loose service coupling, simplified maintenance, and reliable asynchronous processing.

---

## V. Challenges, Troubleshooting & Technical Experience

Several technical challenges emerged while deploying the processing pipeline.

Initially, Amazon EventBridge did not receive upload events because EventBridge notifications were not enabled on the Amazon S3 bucket. After enabling this feature, upload events were successfully published.

Another issue occurred when AWS Step Functions attempted to create MediaConvert jobs. The execution role lacked sufficient IAM permissions, causing workflow failures. Updating the IAM Role and Trust Policy resolved the problem.

The team also experienced incorrect EventBridge Pipes configuration, preventing messages from being forwarded from Amazon SQS to AWS Step Functions. After reviewing the source and target configuration, automatic workflow execution functioned correctly.

These issues highlighted the importance of carefully configuring IAM permissions and validating every integration point within an event-driven architecture.

---

## VI. Evaluation & Professional Reflection

The tenth week significantly strengthened the team's understanding of AWS event-driven application development.

Instead of relying on tightly coupled backend services, the implemented architecture separates each responsibility into an independent AWS service. This design increases scalability while simplifying maintenance and future expansion.

Working with Amazon EventBridge, Amazon SQS, EventBridge Pipes, AWS Step Functions, and AWS Elemental MediaConvert provided valuable practical experience in building distributed cloud applications capable of handling asynchronous workloads efficiently.

The successful deployment of the processing pipeline established the technical foundation required for implementing the complete Video-on-Demand platform.

---

## VII. Plan for Next Week

During the following week, the team will focus on developing the web application and integrating it with the backend services.

The planned activities include:

- Develop the user interface.
- Integrate backend REST APIs.
- Implement the video upload feature.
- Display video metadata.
- Monitor processing status.
- Implement HLS video playback.
- Build the system dashboard.
- Perform integration testing between the frontend and backend.
- Prepare the system for final testing.