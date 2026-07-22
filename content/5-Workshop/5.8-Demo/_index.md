---
title: "System Demo"
date: 2026-07-20
weight: 8
chapter: false
pre: "<b>5.8. </b>"
---

# System Demo

## Overview

After completing the implementation and testing phases, the **Serverless Video-on-Demand Platform on AWS** successfully fulfills all core MVP requirements. The following video demonstrates the complete workflow of the system, from uploading a video through the web application to automatic processing on AWS and final playback on the platform.

## Demonstration Workflow

The demonstration includes the following features:

- User authentication.
- Uploading a video through the web application.
- Storing the original video in the Amazon S3 Raw Upload Bucket.
- Video processing using AWS Elemental MediaConvert.
- Storing the processed video in the Amazon S3 Processed Media Bucket.
- Updating video metadata in Amazon DynamoDB.
- Playing the processed video through the web application.

## Demonstration Video

<video width="100%" controls preload="metadata">
    <source src="/images/5-Workshop/Demo.mp4" type="video/mp4">
</video>

<p align="center">
<i><b>Video 5.1.</b> Demonstration of the Serverless Video-on-Demand Platform on AWS.</i>
</p>

## Result

The demonstration confirms that the complete serverless workflow operates successfully. After a user uploads a video, the system automatically performs media processing, stores the processed output, updates the video metadata, and makes the video available for playback through the web application without requiring any manual intervention.