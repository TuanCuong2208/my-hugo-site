---
title: "System Demo"
date: 2026-07-20
weight: 8
chapter: false
pre: "<b>5.8. </b>"
---


## Overview

After completing the implementation and testing phases, the **Serverless Video-on-Demand Platform on AWS** successfully fulfills all core MVP requirements. The following demonstration video presents the complete workflow of the system, from uploading a video through the web application, processing it on AWS, and making it available for playback on the website.

## Demonstration Workflow

The demonstration covers the complete system workflow, including:

- User authentication.
- Uploading a video through the Web Application.
- Verifying the uploaded video in the Amazon S3 Raw Upload Bucket.
- Monitoring the video processing job using AWS Elemental MediaConvert.
- Verifying the processed video in the Amazon S3 Processed Media Bucket.
- Confirming that the video metadata has been updated in Amazon DynamoDB.
- Playing the processed video through the Web Application.

## Demonstration Video

👉 **Watch the demonstration video here:**

**https://drive.google.com/file/d/1s9Y2AWsQQOhL2RLT8i8CPeO8E06Zf7a8/view?usp=drive_link**

> **Video 5.1.** Demonstration of the complete workflow of the Serverless Video-on-Demand Platform on AWS.

## Result

The demonstration confirms that the system operates successfully according to the designed serverless architecture. After a user uploads a video, the platform automatically processes the media, stores the processed output, updates the corresponding metadata, and makes the video available for playback through the web application. This demonstrates the successful integration and end-to-end operation of all core AWS services within the proposed architecture.