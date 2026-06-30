---
title: "Week 6: Database Migration, Analytics Platforms, and NoSQL Modeling"
date: 2026-05-26
weight: 6
chapter: false
pre: "<b> 1.6. </b> "
---

### I. Executive Summary
This week focuses on database modernization and constructing advanced data analytics ecosystems on AWS cloud infrastructure. The core activities cover cloud database migration processes utilizing AWS DMS and SCT, efficient Data Lake infrastructure setup with AWS Glue, and optimization of NoSQL access pattern designs on DynamoDB. Lastly, it details building an end-to-end Big Data analytics pipeline integrating data ingestion (Kinesis), processing (EMR), and reporting visualization (QuickSight).

### II. Strategic Objectives
* **Database Migration:** Mastering schema conversion workflows and securely automating data migration tasks from legacy systems to AWS.
* **Data Lake Architecture:** Building and managing a centralized data repository, automated through a Data Catalog to classify structured/semi-structured data for analytical tasks.
* **NoSQL Optimization:** Gaining deep knowledge of Single-table design concepts and maximizing query performance based on real-world application access patterns in DynamoDB.
* **Analytics Automation:** Establishing a comprehensive end-to-end Data Pipeline, seamlessly streaming live operations data straight into functional interactive business dashboards.

### III. Activity Log & Detailed Roadmap (From 26/05/2026 to 01/06/2026)

| Timeframe | Activity Category | In-depth Operational Tasks Executed | Results / Deliverables Achieved |
| :--- | :--- | :--- | :--- |
| **Day 1** *(26/05)* | Database Migration | Deploy Lab 43: Utilize AWS Schema Conversion Tool (SCT) to convert schema structures and configure AWS Database Migration Service (DMS) for live replication. | Automated database migration pipeline established successfully between source and target DB. |
| **Day 2** *(27/05)* | Data Lake Lifecycle | Deploy Lab 35: Architect a centralized data storage pool on Amazon S3 and configure AWS Glue Crawler to index metadata into the Glue Data Catalog. | Centralized Data Lake environment ready to serve structured and semi-structured schema mapping. |
| **Day 3** *(28/05)* | NoSQL Data Modeling | Deploy Lab 39: Implement advanced Primary Key, Partition Key, Sort Key, and Secondary Indexes (GSI/LSI) modeling strategies on Amazon DynamoDB. | Standardized data schema ready, minimizing RCUs/WCUs consumption while maximizing query response times. |
| **Day 4** *(29/05)* | Cost & Query Analytics | Deploy Lab 40: Implement AWS Glue in conjunction with Amazon Athena to execute serverless ad-hoc standard SQL queries over system logs stored in S3. | Detailed system operational reports extracted, validating performance benchmarks and cost optimization. |
| **Day 5-6** *(30-31/05)*| End-to-End Analytics | Deploy Lab 72: Integrate full AWS analytical platform suite combining Amazon Kinesis (ingestion), Amazon EMR (distributed processing), and Amazon QuickSight. | Stream processing platform implemented successfully with functional real-time analytical dashboards. |
| **Day 7** *(01/06)* | Audit & Packaging | Consolidate all engineering technical documentation, validate screenshot asset pathways, and execute final web deployment via Hugo framework. | Week 6 worklog portfolio running live and fully optimized on GitHub Pages. |

### IV. In-depth Technical Execution & Analysis

#### 1. Lab 43: AWS Database Schema Conversion Tool and Database Migration Service
****1. Technical Overview****
This lab illustrates the systematic process of a heterogeneous database migration onto the AWS cloud infrastructure. The process utilizes the AWS Schema Conversion Tool (SCT) to analyze database engine compatibility and automatically convert schema definitions (such as views, stored procedures, and functions). Following the conversion, the AWS Database Migration Service (DMS) drives data sync tasks using a managed Replication Instance to execute initial loads (Full Load) and continuous replication (CDC), successfully eliminating system migration downtime.

****2. Execution Process****
* **Step 1: Ingestion Infrastructure Setup:** Launch a managed Replication Instance in the AWS DMS environment acting as the main migration execution engine. Define connectivity configurations (Source Endpoints for local databases and Target Endpoints for AWS cloud databases) and run connectivity validation checks.
* **Step 2: Schema Conversion using AWS SCT:** Install and utilize the desktop-based AWS SCT application to connect to the source engine, generate a detailed Migration Assessment Report to spot any code incompatibilities, convert the database schema, and apply it directly onto the target database.
* **Step 3: Database Migration Task Configuration:** Create and configure a DMS Replication Task specifying the desired migration type, implement strict Table Mappings rules to accurately isolate data tables to sync, and monitor the operation execution until the task transitions to a completed state.

****3. Proofs****
* **1.png:** Configuration screen showing the AWS SCT desktop application interface, showcasing the Migration Assessment Report metrics along with source and target database schema structures mapped after translation.
* **2.png:** Configuration screen showing active Endpoint statuses in the AWS DMS Management Console, validating both Source and Target Endpoints display a green `Successful` connectivity status.
* **3.png:** Configuration screen showing the completed Database Migration Task displaying a status of `Load complete`, paired with deep metrics detailing row modification counts synchronized to the destination DB.

---

#### 2. Lab 35: Data Lake on AWS
****1. Technical Overview****
The Data Lake architecture on AWS delivers a highly secure, cost-effective, and infinitely scalable centralized data storage pool capable of housing multi-format corporate assets (structured, semi-structured, and unstructured). The training focuses on utilizing Amazon S3 as the core storage layer integrated with AWS Glue to govern an automated metadata repository (Glue Data Catalog), enabling down-stream computational engines to read data on-the-fly without manual ingest structures.

****2. Execution Process****
* **Step 1: S3 Bucket Topologies Structuring:** Build individual Amazon S3 storage buckets segregated cleanly by architectural ingestion tiers (such as Raw Inbound Zones and Processed Analytical Zones).
* **Step 2: AWS Glue Crawler Orchestration:** Construct an IAM Service Role provisioning specific data read access to S3 assets. Initialize an AWS Glue Crawler targeting the raw storage bucket paths to automate the scanning process.
* **Step 3: Glue Data Catalog Definition:** Run the configured Glue Crawler to trigger automated schema inference over the unstructured raw object sets, automatically parsing logical database tables into the central Glue Data Catalog metadata lake.

****3. Proofs****
* **4.png:** Configuration screen showing the Amazon S3 Storage Console displaying the list of created data buckets and structured inbound file repository directories for the raw Data Lake layer.
* **5.png:** Configuration screen showing structural Table Schema definitions within the AWS Glue Data Catalog after successful Crawler termination, highlighting parsed Column names and inferred Data Types.

---

#### 3. Lab 39: Amazon DynamoDB Immersion Day
****1. Technical Overview****
Amazon DynamoDB is a fully managed, single-digit millisecond latency Key-Value and Document NoSQL database engineered to provide massive scaling. This lab focuses on architectural patterns required for NoSQL modeling at scale, utilizing both Provisioned and On-Demand capacity models, while implementing secondary indexes (GSIs) to decouple workloads and serve highly customized application access patterns efficiently.

****2. Execution Process****
* **Step 1: DynamoDB Table Definition:** Launch a new NoSQL table through the DynamoDB Management Console, selecting optimal capacity configurations and designating specific attribute sets as the vital Partition Key boundary.
* **Step 2: Advanced Access Patterns Design:** Create and engineer functional Global Secondary Indexes (GSIs) to bypass primary key limitations, enabling low-latency alternate data lookup vectors across different tables.
* **Step 3: Query Execution and Performance Validation:** Issue automated data reads using the AWS Console or programmatic CLI actions via AWS CloudShell to validate response structures, verifying operational correctness and checking total consumed RCUs.

****3. Proofs****
* **6.png:** Configuration screen showing table specification configurations inside the DynamoDB Console, explicitly displaying Partition Key/Sort Key arrangements along with active Global Secondary Indexes (GSI) settings.
* **7.png:** Configuration screen showing query returns under the Items view tab in the DynamoDB Console or via AWS CloudShell outputs, confirming query and scan operational outputs.

---

#### 4. Lab 40: Cost and Performance Analysis with AWS Glue and Amazon Athena
****1. Technical Overview****
Coupling AWS Glue metadata curation with Amazon Athena's interactive ad-hoc querying builds an advanced serverless analytics platform optimized for enterprise environments. AWS Glue Crawlers automate schema discovery over raw logs (such as usage log tracking files) sitting in S3, while Amazon Athena provides an on-demand SQL framework to dissect system cost and infrastructure performance logs without any underlying computing infrastructure to maintain.

****2. Execution Process****
* **Step 1: Log Target Glue Crawler Orchestration:** Create and configure a managed Glue Crawler targeted to scan raw operational log paths inside designated Amazon S3 storage infrastructure.
* **Step 2: Columnar Data Format Conversion:** Implement performance optimization techniques by compressing and transforming legacy row-based log objects (like CSV or JSON) into optimized columnar formats (like Parquet) to save scanning overhead.
* **Step 3: Serverless Athena Ad-hoc SQL Interrogation:** Access the Amazon Athena query workspace, link to the Data Catalog table, and compose standard ANSI SQL expressions to pinpoint performance trends.

****3. Proofs****
* **8.png:** Configuration screen showing execution logs of the targeted AWS Glue Crawler shifting to a `Ready` state or confirming a successful indexing run into the metadata store.
* **9.png:** Configuration screen showing the Amazon Athena Query Editor displaying the written SQL statement executed, structural tabular data outputs, and specific computation benchmarks like Execution Time and Data Scanned volumes.

---

#### 5. Lab 72: Analytics on AWS Workshop
****1. Technical Overview****
Building a comprehensive end-to-end Big Data analytics pipeline addresses data processing needs from stream ingestion to business intelligence visualization. This architecture pairs Amazon Kinesis Data Streams for high-velocity streaming intake with an Amazon EMR (Elastic MapReduce) framework to handle distributed computations (via Apache Spark or Hadoop ecosystems) over S3 datasets, culminating in interactive visual reporting via Amazon QuickSight.

****2. Execution Process****
* **Step 1: Kinesis Ingestion Pipeline Initialization:** Deploy a dedicated Kinesis Data Stream pipeline, right-sizing target Shard counts to support continuous throughput requirements from upstream log generators.
* **Step 2: Distributed Processing Cluster Bootstrapping:** Launch an active multi-node Amazon EMR cluster, specifying software configurations and injecting EMR Steps to clean, translate, and dump raw streams into analytical tables.
* **Step 3: Business Intelligence Hookup via Amazon QuickSight:** Authenticate into the QuickSight workspace, generate a functional corporate Data Set mapped to the curated analytics engine, and customize visualization components (Visuals) to form a live dashboard.

****3. Proofs****
* **10.png:** Configuration screen showing the Amazon Kinesis Data Streams monitoring dashboard displaying active CloudWatch metrics, validating stream data throughput entering the cloud architecture.
* **11.png:** Configuration screen showing the finalized, fully functional, and interactive business intelligence analytics dashboard running live inside the Amazon QuickSight workspace environment.

---

### V. Infrastructure Challenges, Error Resolution Logs & Expert Perspectives
*(This section will be analyzed deeply and document engineering challenges encountered during execution once all labs are complete)*

### VI. Professional Reflections
*(This section will capture personal takeaways and architectural evaluations upon completion)*

### VII. Strategic Planning & Optimization Roadmap for Next Week
*(This section will map out upcoming operational objectives based on current implementation feedback)*