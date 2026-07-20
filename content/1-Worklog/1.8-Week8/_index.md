---
title: "Week 8 Worklog"
date: 2026-06-09
weight: 8
chapter: false
pre: "<b> 1.8. </b> "
---

### I. Executive Summary

After completing the initial architecture design of the system in the previous week, the team moved into the technical design refinement phase before beginning the implementation of the project's core functionalities. The primary objective of this week was to review the overall architecture, conduct a deeper analysis of each system component, and determine how every module would be implemented during the development process.

Throughout the research phase, the team continued studying AWS Documentation, AWS Prescriptive Guidance, and several open-source Video-on-Demand projects to evaluate whether the selected architecture was suitable for the project's requirements. Through internal discussions and technical reviews, several architectural components were refined to improve scalability, reduce service coupling, and simplify future implementation.

At the same time, the team began designing the Amazon DynamoDB data model, defining the list of business APIs to be implemented using Amazon API Gateway and AWS Lambda, and identifying the data flow between system components.

By the end of the week, the team had completed the initial version of the technical design documents, establishing a solid foundation for the implementation phase scheduled for the following week.

### II. Strategic Objectives

After establishing the overall system architecture, the primary objective of Week 8 was to transform the high-level design into detailed technical specifications in preparation for system development.

The major objectives included:

- Reviewing and refining the overall architecture through research and internal technical discussions.
- Designing the data model for Amazon DynamoDB.
- Defining business APIs and communication methods between the Frontend and Backend.
- Preparing the project structure and dividing the system into functional modules.
- Creating a detailed implementation roadmap for each development phase.
- Ensuring that all architectural decisions satisfy scalability, performance, and operational cost requirements.

Through these objectives, the team aimed to establish a consistent technical foundation before beginning the implementation of the system.

### III. Activity Log & Detailed Timeline (From June 9, 2026 to June 15, 2026)

| Time | Activity Category | Detailed Technical Tasks | Results / Deliverables |
| :--- | :--- | :--- | :--- |
| **Day 1** *(09/06)* | Architecture Review | Reviewed Architecture Draft V1, validated data flows, and analyzed the responsibilities of each AWS service within the system. | Completed the updated architecture design for the technical design phase. |
| **Day 2** *(10/06)* | Database Design | Designed the Amazon DynamoDB data model, identified the Partition Key, Sort Key, and video metadata attributes. | Completed the preliminary database design. |
| **Day 3** *(11/06)* | API Design | Defined the required APIs, HTTP methods, request/response structures, and authentication workflow using Amazon Cognito. | Finalized the initial API specification for the system's core features. |
| **Day 4** *(12/06)* | Processing Workflow Design | Analyzed the Upload Video, Video Processing, and Video Streaming workflows and defined the data exchanged between AWS services. | Completed the business process workflow. |
| **Day 5** *(13/06)* | Development Environment Preparation | Organized the project structure, source code directories, and prepared development environments for both Backend and Frontend. | Established the initial project structure. |
| **Day 6** *(14/06)* | Development Planning | Divided the system into functional modules and prepared a phased development roadmap. | Completed the detailed implementation roadmap. |
| **Day 7** *(15/06)* | Design Review | Reviewed all technical documentation, finalized implementation decisions, and prepared for the programming phase. | Completed the technical design documentation for the project. |

### IV. In-depth Technical Execution & Analysis

Following the completion of the initial system architecture design in the previous week, the team focused on refining the technical design to prepare for the implementation phase. Rather than developing application features immediately, this week's objective was to transform the high-level architecture into detailed technical specifications that could be directly applied during development.

Throughout the research process, the team continued studying the official AWS Documentation, the AWS Well-Architected Framework, and several open-source Video-on-Demand projects to validate the proposed architecture. By comparing different implementation approaches, the team refined several architectural components to simplify data processing, reduce service coupling, and improve long-term scalability.

One of the primary objectives this week was designing the system's data model. After analyzing the project's business requirements, the team decided to continue using Amazon DynamoDB as the primary database for storing video metadata. The proposed schema includes fields such as Video ID, Video Name, Upload Time, Processing Status, Owner, Category, and references to processed video assets. The team also began researching the use of Global Secondary Indexes (GSIs) to support future query patterns such as filtering by processing status or video category.

In parallel, the team defined the initial set of APIs that would be implemented during the first development phase. These APIs were grouped into several functional categories, including Authentication, Video Management, and Video Streaming. For each endpoint, the team specified the HTTP method, request and response structures, and the planned authentication mechanism using Amazon Cognito.

Regarding the video processing workflow, the team continued analyzing the interactions among Amazon S3, Amazon SQS, AWS Lambda, and AWS Elemental MediaConvert. Instead of allowing the Backend to directly handle the entire upload and transcoding process, the team maintained the asynchronous processing approach in order to reduce API workload and improve the overall scalability of the system.

Beyond database and API design, the team also established the initial project structure to maintain consistency throughout development. The Backend and Frontend were organized as separate projects, making development and testing more manageable. In addition, clear boundaries were defined for modules such as Authentication, Video Upload, Video Processing, and Video Streaming to facilitate future implementation.

By the end of the week, although no production features had been developed yet, the team completed most of the technical design documentation required for the project. This preparation is expected to significantly reduce technical risks during implementation while providing a solid foundation for the upcoming development stages.

### V. Infrastructure Challenges, Issue Log & Technical Insights

During the technical design phase, the team realized that building a Serverless system involves much more than simply selecting AWS services. A successful architecture requires clearly defining the responsibilities of every component. Without a consistent design from the beginning, independently developed modules could easily become incompatible, particularly between the Backend, database, and event-driven workflows.

One of the primary challenges discussed by the team was designing the data model for Amazon DynamoDB. Unlike traditional relational databases, DynamoDB requires schemas to be designed around access patterns rather than normalization principles. As a result, the team spent considerable time identifying an appropriate Partition Key, selecting attributes that should be indexed, and planning how the database could scale as the application grows.

Another important discussion focused on API design consistency. The team agreed to adopt a RESTful API architecture and established common conventions for endpoint naming, JSON request and response formats, and HTTP status codes. Defining these standards before implementation will help maintain consistency across all Backend services.

In addition to technical design decisions, the team also considered the long-term scalability of the platform. Instead of designing the system solely for the current project scope, the architecture was planned so that future features—such as Video Recommendation, Comments, or Playlists—could be integrated with minimal modifications to the existing infrastructure.

Through continuous research and internal technical discussions, the team concluded that investing sufficient time in the design phase would substantially reduce implementation risks while creating a more maintainable and scalable system architecture.

### VI. Professional Reflection

Week 8 provided the team with a much deeper understanding of the importance of the design phase in the development lifecycle of a cloud-native application. Although no business features were implemented during this period, designing the database schema, defining APIs, and mapping data flows between AWS services helped the team build a much clearer picture of how the entire platform would operate once development begins.

By studying AWS best practices and reviewing real-world projects, the team also recognized that a well-designed architecture should not only satisfy current functional requirements but also support future scalability, maintainability, and operational efficiency. Decisions made during the design stage will directly influence system performance, operational costs, and long-term extensibility.

This week's activities also strengthened the team's ability to analyze requirements, design technical solutions, and collaborate effectively throughout a software engineering project. Establishing shared technical standards before implementation was considered an essential step toward minimizing major architectural changes during development.

Overall, although the team did not produce any deployable software this week, a comprehensive technical foundation was successfully established, allowing the project to move confidently into the implementation phase.

### VII. Strategic Plan & Roadmap for Next Week

During the following week, the team plans to officially begin implementing the system based on the technical design documents completed over the past two weeks.

The primary focus will be preparing the AWS infrastructure required for development, including configuring core services such as Amazon Cognito, Amazon S3, Amazon DynamoDB, Amazon API Gateway, and AWS Lambda. At the same time, the team will begin implementing the project's foundational modules, including user authentication, database connectivity, and the initial APIs for video management.

Alongside Backend development, each module will be tested immediately after implementation to ensure stability before integration with other system components. Developing the project incrementally will enable the team to identify potential issues early and make architectural adjustments when necessary without affecting the overall system.

The main objective for the upcoming week is to complete the initial technical foundation of the platform, paving the way for implementing the Video Upload workflow and the Video Processing Pipeline during the subsequent stages of the project.