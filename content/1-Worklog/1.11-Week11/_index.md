---
title: "Week 11 Worklog"
date: 2026-06-30
weight: 11
chapter: false
pre: "<b>1.11. </b>"
---

## I. General Overview

Following the successful implementation of the Video Processing Pipeline, the eleventh week focused on developing the **Web Application** and integrating it with the serverless backend. The objective was to provide users with an intuitive interface for authentication, video upload, video management, and online video streaming.

During this week, the team completed the application's core pages, integrated backend APIs, and connected the web interface with Amazon API Gateway, AWS Lambda, Amazon DynamoDB, and Amazon S3. The application was also integrated with Amazon CloudFront to deliver processed HLS videos efficiently.

In addition to feature development, multiple integration tests were performed to verify communication between the frontend and backend services. By the end of the week, the application successfully supported the complete workflow from user login to video playback.

---

## II. Weekly Objectives

The objectives for this week included:

- Complete the web application interface.
- Implement user authentication.
- Integrate backend REST APIs.
- Implement video upload functionality.
- Display uploaded videos.
- Monitor processing status.
- Implement HLS video playback.
- Build the management dashboard.
- Perform frontend-backend integration testing.
- Prepare the platform for system-wide testing.

---

## III. Activity Log & Weekly Schedule (30/06/2026 – 06/07/2026)

| Time | Activity | Description | Result |
|------|----------|-------------|--------|
| **Day 1 (30/06)** | User Interface Development | Designed and completed the login page, upload page, video list, and dashboard layout. Optimized the user workflow to improve usability. | Core interface completed successfully. |
| **Day 2 (01/07)** | Backend API Integration | Connected the web application with Amazon API Gateway to access APIs for Presigned URL generation, metadata storage, and video retrieval. | Frontend successfully communicated with backend services. |
| **Day 3 (02/07)** | Video Upload | Implemented direct video upload using Presigned URLs. Added upload progress indicators and verified successful uploads to Amazon S3. | Video upload function operated correctly. |
| **Day 4 (03/07)** | Video Management | Retrieved metadata from Amazon DynamoDB and displayed uploaded videos together with their processing status. | Video list displayed accurate information. |
| **Day 5 (04/07)** | Video Playback | Integrated an HLS player using processed video files delivered through Amazon CloudFront. | Videos streamed successfully in the browser. |
| **Day 6 (05/07)** | Dashboard Development | Completed the dashboard for monitoring uploaded videos and processing progress. Improved layout consistency and responsiveness. | Dashboard functioned correctly. |
| **Day 7 (06/07)** | Integration Testing | Tested the complete workflow from authentication and upload to video processing and playback. | End-to-end workflow operated successfully. |

---

## IV. Technical Implementation & Detailed Analysis

The primary objective during this week was integrating all previously developed AWS services into a single web application that users could interact with easily. Instead of accessing AWS resources directly, users perform every operation through the application interface, while backend services process requests transparently.

The application communicates with Amazon API Gateway to invoke backend APIs implemented using AWS Lambda. These APIs handle operations such as generating Presigned URLs, storing metadata, and retrieving video information from Amazon DynamoDB.

For video uploads, the application first requests a Presigned URL from the backend. After receiving the URL, the browser uploads the selected video directly to the Amazon S3 Raw Upload Bucket. This design minimizes backend workload because large media files never pass through AWS Lambda.

Once the upload is completed, the event-driven processing pipeline begins automatically. During processing, the application periodically retrieves updated metadata from Amazon DynamoDB to display the current processing status for each uploaded video.

After transcoding finishes, AWS Elemental MediaConvert generates HLS output files that are stored in the Amazon S3 Processed Media Bucket. These files are distributed through Amazon CloudFront, enabling low-latency and reliable video streaming.

A management dashboard was also implemented to provide users with an overview of uploaded videos, processing status, and available media. The dashboard simplifies system monitoring while improving the overall user experience.

By the end of the week, all major frontend features had been integrated successfully with the serverless backend, resulting in a complete and functional Video-on-Demand web application.

---

## V. Challenges, Troubleshooting & Technical Experience

During integration, several synchronization issues appeared between the frontend interface and backend services.

Initially, some API responses contained inconsistent data structures, preventing the application from displaying video information correctly. After standardizing the response format returned by AWS Lambda, the interface displayed metadata successfully.

Another issue involved video playback. The application occasionally attempted to load HLS playlists before MediaConvert had completed transcoding. The team modified the metadata validation process so that playback became available only after processing was fully completed.

Additional improvements were made to the dashboard by refreshing processing status periodically instead of requiring manual page reloads. These enhancements significantly improved usability and provided a smoother user experience.

The integration process reinforced the importance of maintaining consistent API design and reliable communication between frontend applications and serverless backend services.

---

## VI. Evaluation & Professional Reflection

The eleventh week represented the transition from backend infrastructure to a complete end-user application.

The team successfully combined Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon S3, Amazon CloudFront, and the previously implemented processing pipeline into a unified web platform capable of supporting the entire video streaming workflow.

This experience provided valuable knowledge about integrating frontend applications with cloud-native backend architectures while maintaining scalability, performance, and maintainability.

The completed application also demonstrated the practical advantages of serverless development by reducing infrastructure management and simplifying application deployment.

---

## VII. Plan for Next Week

During the final week of the internship, the team will focus on validating the complete platform and preparing the project for completion.

The planned activities include:

- Perform comprehensive system testing.
- Verify backend functionality.
- Test the complete video processing pipeline.
- Evaluate web application performance.
- Optimize AWS resource configuration.
- Resolve remaining issues.
- Complete technical documentation.
- Finalize the internship report.
- Prepare the project for presentation and final evaluation.