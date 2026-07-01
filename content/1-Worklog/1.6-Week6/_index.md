---
title: "Week 6: Analytics Platforms and NoSQL Data Modeling"
date: 2026-05-26
weight: 6
chapter: false
pre: "<b> 1.6. </b> "
---

### I. Executive Summary
This week focuses on modernizing cloud storage layers and building advanced data analytics infrastructures within the AWS ecosystem. The core architectural elements cover constructing automated Data Lake pipelines using Amazon S3 and AWS Glue, and designing highly optimized NoSQL database storage models using Amazon DynamoDB. Lastly, it details establishing an end-to-end distributed Big Data analytics ecosystem combining data stream ingestion (Kinesis), parallel distributed computing (EMR), and analytical reporting dashboards (QuickSight).

### II. Strategic Objectives
* **Data Lake Architecture:** Structuring centralized enterprise repositories and automating schema ingestion patterns via the Glue Data Catalog to drive deep data analysis.
* **NoSQL Optimization:** Master advanced single-table design concepts and optimize query execution plans against high-scale application access patterns inside DynamoDB.
* **Analytics Automation:** Deploying an end-to-end automated analytical data stream, securely translating raw unformatted transactional inputs into business intelligence charts.

### III. Activity Log & Detailed Roadmap (From 26/05/2026 to 01/06/2026)

| Timeframe | Activity Category | In-depth Operational Tasks Executed | Results / Deliverables Achieved |
| :--- | :--- | :--- | :--- |
| **Day 1-2** *(26-27/05)* | Data Lake Lifecycle | Deploy Lab 35: Structure a centralized data repository on Amazon S3 and configure an AWS Glue Crawler to sync structural metadata into the Glue Data Catalog. | Centralized Data Lake environment ready to serve structured and semi-structured automated mappings. |
| **Day 3** *(28/05)* | NoSQL Data Modeling | Deploy Lab 39: Implement advanced Primary Key, Partition Key, Sort Key, and Secondary Index (GSI) single-table modeling blueprints on Amazon DynamoDB. | Standardized data schema ready, minimizing RCUs/WCUs consumption while maximizing query response times. |
| **Day 4** *(29/05)* | Cost & Query Analytics | Deploy Lab 40: Orchestrate an AWS Glue metadata pipeline and configure Amazon Athena to execute serverless standard ANSI SQL actions over raw S3 system logs. | Detailed system operational reports extracted, validating performance benchmarks and infrastructure cost trends. |
| **Day 5-6** *(30-31/05)*| End-to-End Analytics | Deploy Lab 72: Build an end-to-end analytical data stream pipeline aggregating Amazon Kinesis (ingestion), Amazon EMR (processing), and Amazon QuickSight. | Stream processing platform implemented successfully with functional real-time analytical business dashboards. |
| **Day 7** *(01/06)* | Finalization | Consolidate engineering technical writeups, standardize screenshot media asset mapping rules, and execute web updates via the Hugo framework. | Week 6 worklog portfolio running live and fully optimized on GitHub Pages. |

### IV. In-depth Technical Execution & Analysis

#### 1. Lab 35: Data Lake on AWS

**1. Technical Overview**
The Data Lake architecture on AWS delivers a highly secure, cost-effective, and infinitely scalable centralized data storage pool capable of housing multi-format corporate assets. This training module emphasizes structuring raw file inbound paths within Amazon S3 bucket storage layers combined with managed AWS Glue orchestration engines to parse metadata schemas directly into the unified Glue Data Catalog, allowing downstream ad-hoc analytical execution.

**2. Execution Process**
* **Step 1: Inbound S3 Architecture Provisioning:** Spin up targeted Amazon S3 buckets acting as the primary secure raw data landing zones for incoming objects.
* **Step 2: AWS Glue Crawler Orchestration:** Configure appropriate IAM execution roles and deploy an automated Glue Crawler directed at the source S3 bucket directory.
* **Step 3: Data Catalog Sync Enforcement:** Execute the deployed Crawler configuration to analyze file layout formats, triggering automated schema inference and cataloging structural logical tables.

**3. Proofs**
* **1:** Configuration screen showing the Amazon S3 Management Console, verifying active data lake storage buckets created successfully inside the current AWS region.
<img src="/images/week6/1.png" alt="S3 Buckets List" style="max-width:100%; height:auto;" />
* **2:** Configuration screen showing the detailed view of file asset layouts or active raw object directories sitting within the primary S3 storage container.
<img src="/images/week6/2.png" alt="S3 Bucket Objects View" style="max-width:100%; height:auto;" />

---

#### 2. Lab 39: Amazon DynamoDB Immersion Day

**1. Technical Overview**
Amazon DynamoDB is a fully managed, single-digit millisecond latency Key-Value and Document NoSQL database engineered to handle massive internet-scale operations. The deep-dive exercises focus extensively on translating real-world relational access patterns into optimal single-table NoSQL designs by choosing high-cardinality Partition Keys, complementary Sort Keys, and active Global Secondary Indexes (GSIs).

**2. Execution Process**
* **Step 1: DynamoDB Table Structure Provisioning:** Create a fresh NoSQL table instance via the DynamoDB Console, designating core string schemas as the main Partition Key configuration.
* **Step 2: Alternate Access Pattern Indexing:** Design and initialize Global Secondary Indexes (GSIs) to decouple application query parameters and unlock flexible indexing alternatives.
* **Step 3: Transaction Operations Testing:** Use programmatic actions or AWS CloudShell terminal structures to insert trial items (PutItem) and execute targeted Query and Scan evaluations.

**3. Proofs**
* **3:** Configuration screen showing table properties metrics in the DynamoDB Console, verifying active Partition Key, Sort Key, and table resource sizing profiles.
<img src="/images/week6/3.png" alt="DynamoDB Table Configuration" style="max-width:100%; height:auto;" />
* **4:** Configuration screen showing the active Console Items view interface, validating target query metrics returned data rows successfully following a conditional Query call.
<img src="/images/week6/4.png" alt="DynamoDB Query Results" style="max-width:100%; height:auto;" />

---

#### 3. Lab 40: Cost and Performance Analysis with AWS Glue and Amazon Athena

**1. Technical Overview**
Coupling AWS Glue metadata curation with Amazon Athena's interactive ad-hoc querying builds a serverless analytics model that cuts downstream infrastructure management overhead. AWS Glue Crawlers handle the heavy-lifting of scanning and creating schema blueprints over unstructured application usage tracking text log files inside S3, while Amazon Athena applies a serverless execution runtime to query logs using standard SQL.

**2. Execution Process**
* **Step 1: Log Target Glue Crawler Mapping:** Instantiate an enterprise Glue Crawler configuration targeted strictly to scan underlying row-based raw system logs on S3.
* **Step 2: Columnar Serialization Enforcement:** Leverage high-performance processing strategies by converting unstructured payloads into optimized Apache Parquet layouts to scale down processing costs.
* **Step 3: Serverless Ad-hoc SQL Query Interrogation:** Open the interactive Amazon Athena Query Editor interface, connect to the mapped catalog table, and run query scripts.

**3. Proofs**
* **5:** Configuration screen showing the execution lifecycle of the operational Glue Crawler, confirming a completed run cycle status into the centralized catalog.
<img src="/images/week6/5.png" alt="AWS Glue Crawler Status" style="max-width:100%; height:auto;" />
* **6:** Configuration screen showing the Amazon Athena Query Editor interface displaying a successful SQL execution query string alongside tabular returned outputs and total execution metrics.
<img src="/images/week6/6.png" alt="Amazon Athena Query Editor" style="max-width:100%; height:auto;" />

---

#### 4. Lab 72: Analytics on AWS Workshop

**1. Technical Overview**
Deploying an end-to-end analytics data streaming pipeline tackles complex high-scale corporate data processing from pipeline ingestion straight down to interactive boardroom presentation. The pipeline maps Amazon Kinesis Data Streams for high-velocity log ingest actions, transfers payloads onto multi-node Amazon EMR (Elastic MapReduce) clusters for Apache Spark cluster processing, and establishes data feeds into Amazon QuickSight for intelligence reports.

**2. Execution Process**
* **Step 1: Streaming Ingest Ingress Orchestration:** Initialize an operational Amazon Kinesis Data Stream pipeline, tuning individual component Shard allocations to sustain incoming traffic streams.
* **Step 2: Parallel Computing Cluster Bootstrapping:** Spin up a managed Amazon EMR cluster structure, mapping distinct data processing steps (EMR Steps) to convert unstructured inbound stream chunks.
* **Step 3: BI Dashboard Visualizations Alignment:** Log into the corporate Amazon QuickSight console space, mount the underlying analyzed dataset layer, and structure interactive graphic components (Visuals).

**3. Proofs**
* **7:** Configuration screen showing CloudWatch ingestion tracking metrics inside the Kinesis Console, verifying continuous data intake across active stream pipes.
<img src="/images/week6/7.png" alt="Kinesis Stream Data Metrics" style="max-width:100%; height:auto;" />
* **8:** Configuration screen showing the complete interactive Business Intelligence reporting dashboard setup operating inside the corporate Amazon QuickSight instance environment.
<img src="/images/week6/8.png" alt="Amazon QuickSight Dashboard View" style="max-width:100%; height:auto;" />

---

### V. Infrastructure Challenges, Error Resolution Logs & Expert Perspectives
*(This section will document infrastructure errors and engineering mitigation actions once the implementations are finalized)*

### VI. Professional Reflections
*(This section will summarize technical conclusions and engineering insights learned upon week closure)*

### VII. Strategic Planning & Optimization Roadmap for Next Week
*(This section will define आगामी target operational goals for next week's architecture expansion)*