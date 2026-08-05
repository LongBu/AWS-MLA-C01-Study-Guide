## AWS-SAA-C01-Study-Guide

Note these are my own personal notes and are a work in progress as I study towards passing this exam.  If this helps someone great, but I make no guarantees/promises.  

## Table of Contents
1. <a href="#introduction">Introduction</a>

## Introduction
<a href="https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS_Certified_Solutions_Architect_Associate-Exam_Guide_EN_1.8.pdf">AWS Certified Solutions Architect Associate (SAA-C01) Exam Guide</a>

<a href="https://certmetrics.com/amazon/candidate/benefit_summary.aspx">Don't forget to utilize a benefit code if you've passed another AWS exam previously to save</a>

### Exam Content Breakdown:

| Domain  | % of Exam |
| ------------- | ------------- |
| Domain 1: Design Resilient Architectures | 34%  |
| Domain 2: Define Performant Architectures | 24%  |
| Domain 3: Specify Secure Applications and Architectures | 26% |
| Domain 4: Design Cost-Optimized Architectures  | 10% |
| Domain 5: Define Operationally Excellent Architectures  | 6% |
| **Total** | **100%** |

  * 170 minutes 
  * 65 questions
  * \>= 72% to pass
  * Good to use the bathroom before the exam
  * Average question time should be between 2 and 2 1/2 minutes
  * Try to understand each question thoroughly


# Sagemaker (SM)
## SM Pipeline
  * name, steps, and parameters
  * designed to be scale orchestrations up to tens of thousands of complex ML workflows
  * ensures automation and reproducibility
  * parameters can have default values, but may also be overridden during pipeline execution

## SM Studio
  * Tagging SM resources within a SM Studio domain allows cost tracking per user or team. AWS Budgets can then monitor these tags and send alerts when usage exceeds a defined threshold.
  * SM Studio Notebooks provide persistent storage, allowing users to manage multiple notebooks, store datasets, and access them later allowing better management of ML projects
  * SM Studio and standalone notebook instances support popular machine learning libraries (e.g., TensorFlow, PyTorch), as these are pre-installed in both.

## SM Domain
  * A logical container that groups users, shared storage, and execution resources, enabling collaboration and centralized management for ML development teams.
	 
## SM Feature Store 
  * stores versions of features so as to allow tracking of changes over time, ensuring reproducibility of model accuracy via historical features
  * serves features for both training and real-time inference, ensuring feature consistency and lineage
  * offline versus online

## SM script mode
  * run custom training scripts inside managed prebuilt SM containers
  * allows the use of AWS infrastructure to enable scaling, distribute training and logging

## SM serverless inference

## SM Autopilot
  * automates the entire ML workflow from data preprocessing to model training and tuning
  * Automates:
    * Algorithm selection
    * Data preprocessing
    * ﻿Model tuning
    * All infrastructure
  * It does all the trial & error for you
  * More broadly this is called AutoML

## SM Experiments
  * Best way to organize and track steps of a trial, utilize *trial components* within trials to represent different stages or steps of a workflow within a trial (eg: data preprocessing, model training, evaluation) so as to track each step separately and compare results across trials
  * Primary benefit of using in a ML workflow is the ability to capture and organize detailed metadata for each trial, ensuring fidelity of reproduction as they were run, which is critical for collaboration/moving models to production
  * Tracks which datasets, hyperparameters, configurations used in the experiments that produced the models, allowing tracibility and performance evaluation
  * offers an API and a graphical interface in SM Studio, allowing visualization and comparison of key performance metrics (eg: accuracy and loss) across different trials to identify the best performing model.

## SM Canvas
  * Service for non-coders to build models
  * Doesn't provide comprehensive data preparation and transformations (if needed, use Data Wrangler)

## SM Clarify
  * A tool for detecting bias and explaining model predictions, ensuring fairness and transparency in machine learning models.

## Multi-Model Endpoints
  * available via SM
  * host multiple models on a single endpoint
  * single container and instance fleet, which might have varying degrees of usage (infrequent to frequent) to dynamically load models on demand
  * reduces cost
  * improves resource utilization (reduce per-model overhead, optimize memory usage)

## SM Categories of built-in algorithm:
  * supervised
  * unsupervised
  * textual analysis
  * image classification

## SM Algorithms
### Supervised vs Unsupervised Algorithms
  * Unsupervised:
    * Singular Value Decomposition (SVD)
    * Random Cut Forest
    * Neural Topic Model
    * LDA
    * K-Means
    * PCA
    * IP Insights
    * BlazingText (Word2vec)
  * Supervised:
    * Factorization Machines
    * KNN
    * Semantic Segmentation
    * Image Classification
    * Object Detection
    * Object2Vec
    * Deep AR Forecasting
    * Seq2Seq
    * BlazingText (Text Classification)
    * XGBoost
    * Linear Learner
    * Decision Trees
    * Naive Bayes
    * Logistic Regression
    * Recommendation Engine (ALS)
    * Support Vector Machine (SVM)
  * Neither: Reinforcement Learning

### Image classification
  * Assign one or more labels to an image
  * Not as well suited to detect multiple objects in an image as Object Detection, due to the lack of placement context
  * Allows teams (even those inexeperienced) to focus on quickly building and deploying a ML model for image classification without managing the infrastructure.

### Object Detection
  * Identify/Locate all objects in an image with bounding boxes

### Semantic Segmentation
  * Pixel-level object classification

### XGBoost
  * Effective at working with highly imbalanced data
  * Provides a strong balance between accuracy and traceability of feature importance and how it influences predictions (much the case for other Tree-based algorithms)

### Decision Tree Regression 
  * predicts continuous values
 
### Classification Trees 
  * used for binary classification.

### Linear Learner
  * predicts continuous numerical outcomes and is not appropriate for binary classification tasks.
  * most effective approach to establish a simple, interpretable performance baseline to evaluate against more complex models in SM utilizing the same data
  * Effective at training with highly (class) imbalanced data, which can be mitigated by either the 'balance_multiclass_weights' or 'class_weights' hyperparameters.  This is more apropos over XGBoost if per class weighting is the ask.

### Logistic regression
statistical method designed for binary classification problems

# Amazon Bedrock
  *  A fully managed AWS service that provides access to foundation models (FMs) from various providers, allowing developers to build and scale generative AI applications without managing underlying infrastructure.
  * Model caching can improve performance and consistency for repeated questions
  * Lowering the temperature via the Amazon Bedrock API and reducing the top-K parameter limits randomness in token selection, leading to more deterministic and consistent responses from the LLM.
  * Retrain the LLM (aka: fine tune the FM [not from scratch]) with a retail-specific dataset to improve consistency in responses related to product information and return policies.


# Data mesh architecture
  * data as a product with the decentralized data ownership and domain oriented architecture

# AWS Well-Architected Framework/Tool:

  * Pillars:
    * Operational excellence-run/monitor system/assets=>increase business value through RA/mitigation
    * Security-protect=>increase business value through RA/mitigation
    * Reliability-recover, dynamically allocate, mitigate despite misconfiguration/problem(s)
    * Performance-meet system requirements and maintenance through changes
    * Cost optimization-deliver at lowest price point
    * Sustainability-minimize environmental impact
  * Tool scans workloads for these criteria

# Kinesis
## kinesis producer Lib (KPL)
  * main advantage over custom AWS SDK coding: improved error handling and data throughput

## Kinesis Data Streams 
  * shard: a processing unit with a fixed data throughput capacity
  * able to scale and handle varying loads
  * combined with AWS Lambda allows for real-time data processing and auto-scaling capabilities

## Kinesis Data Analytics 
  * Managed Apache Flink provides robust analytics capabilities
  * Not inherently the best solution for direct, real-time responsiveness integrated with Lambda (look to Kinesis Data Streams for this)

## Amazon Firehose
  * designed to deliver streaming data into AWS services (eg: S3, Redshift)
  * provides real-time data ingestion
  * configured buffer data based on time intervals helps in batch processing, which reduces API calls and helps maintain data consistency.

## Amazon Transcribe 
  * speech (audio) to text
  * supports custom vocabularies for improved transcription accuracy (eg: for industry-specific terms)
  * integrates seamlessly with s3
  * scalable and cost-efficient processing
  * Custom vocabulary 
  * auto punctuation ensures transcripts are readable
  * speaker identification distinguishes between speakers.

## Amazon Translate
  * If small volumes of data, orchestrate via Lambda (15 minute limit)
  * If large volumes of data, orchestrate via step functions (up to 1 year limit)
  * Can normalize language, but can't address formatting, noise, missing fields.  Look to glue and Data Wrangler for cleaning and normalization

## AWS Macie
  * Discover and classify sensitive data in S3
  * can trigger AWS Lambda functions to redact or remove sensitive information when added to an S3 bucket, providing an automated, scalable, and low-overhead solution
  * leverages ML to automatically detect, classify, and protect sensitive data/PII
  * most appropriate solution when you need to identify and redact sensitive data stored in S3 before it is accessed or processed with little manual intervention
  * Concerning redaction/removal, other services mentioned, such as AWS Glue, Amazon Comprehend, and AWS DataBrew, are capable of processing and transforming data, but they either:
    * Require manual setup for redaction
    * Are not designed for sensitive data classification
    * Best suited for analytics rather than preprocessing sensitive datasets for ML pipelines.

## Amazon Q Businesss
 * Managed service supporting "AI" coding suggestions per prompts specific to AWS resources/services
 * Supports third-party integration via plugins (eg: Jira, to automate tasks such as ticket creation).
 * Supports APIs for third-party applications (no need for custom APIs)
 * IAM Identity Center provides centralized control over user access and permissions, crucial for managing who can interact with the system.

## Amazon Comprehend (Medical):
  * Serverless NLP service harnessing NLP to uncover valuable insights and connections in text analytics
  * Easier to implement than an NLP model from the ground up
  * Medical version detects PHI via DetectPHI API
  * analyzes only text data (eg: can't process audio/video/pictures)
  * Input social media, emails, web pages, documents, transcripts, medical records (Comprehend Medical)
  * PII/sensitive data identification and redaction, though not optimized for automated, large-scale scanning and redaction of sensitive data stored in S3 with minimal operational overhead.
  * Doesn't offer semantic search or vector embedding (look to Kendra for this)
  * Targeted sentiment (for specific entities)
  * Can train on your own data
  * Can integrate with S3, Firehose, Lambda, Lex (eg realtime sentiment analysis), KMS, etc.
  * Comprehend asynchronous batch designed for large scale analysis from S3, automatically scaling, parallel processing, all with minimal overhead
  * Comprehend real-time inference conducted via API
  * Results of the model are the following:
    * Events detection
    * Key phrases-noun phrases
    * Language
    * Sentiment
    * Syntax-boils down each word into a part of speech
    * Entities-nouns
      * Entity types include: COMMERCIAL_ITEM, DATE, EVENT, LOCATION, ORGANIZATION, OTHER, PERSON, QUANTITY, TITLE
      * Creating a Custom entity recognizer/recognition model can extend beyond the generic Entity types

## Amazon Textract
  * Extracts text, handwriting, and structured data from scanned documents including forms/tables
  * AnalyzeDocument API with the FORMS feature designed to identify and return structured data such as key-value pairs and tables from documents (eg: invoices and receipts)

## Amazon Kendra
  * fully managed
  * intelligent search service
  * utilizes vector embeddings allowing hybrid search (keywords and vector searches), but doesn't offer vector database support.  A vector database being a specialized database for storing and querying vector embeddings (numerical representations of data) to perform similarity or nearest-neighbor searches.
  * supports:
    * semantic search: understands user intent and contextual meaning rather than relying solely on keyword matching, improving relevance in information retrieval
    * natural language queries
  * integrates natively with s3
  * indexes docs so as to provide efficient retrieval of relevant content
  * EventBridge can trigger Lambda to ensure that new documents are indexed in Kendra automatically

## Amazon Rekognition
  * Specializes in Image Analysis (eg: label detection, faces, and objects)
  * Doesn't provide document structure extration

# EMR
  * Big data platform that runs Spark, Hadoop and Presto for large scale data processing/transformations with full control over cluster configuration and resource management.
  * integrates well with Amazon SageMaker Studio, facilitating seamless preprocessing within ML pipelines.

## EMR cluster 
  * can use instance store for ephemeral/transient, cost-effective storage of temporary data
## EMR serverless

# Storage
## EBS
  * block level storage for raw storage(DB, or other)

## EFS
  * file storage

## FSX 
  * Lustre mounted/linked with S3 bucket with fast file mode enabled is optimal for efficient on demand streaming of large (video) files.  Fast file mode in S3 enable streaming without fully downloading large files, reducing storage and overhead.
  * Only FSx for Lustre can be mounted directly for SM training jobs (eg: FSx for NetApp ONTAP cannot be mounted directly as a volume in SageMaker training jobs), so if not Lustre based, copy to S3
  * Mounting is good, but more apt for performance, Fast file mode is key

## S3

### Standard
  * provides low-latency, high throughput, optimized for frequent access (eg: for training or inference)

### Standard-IA
  * suitable for files less frequently accessed, but still need quick access

### Intelligent Tiering
  * optimizes costs for infrequently accessed data or data with unpredictable access patterns
  * not ideal for cost-effectiveness for data known to become infrequently accessed
  * not ideal for datasets that need low-latency (eg: for training or inference)

### Glacier (classes)
  * lower cost, so long as access is seldom, otherwise consider STD/-IA/Intelligent Tiering
  * files are still accessible, but not as fast as non-glacier classes
  
## Database

### Redshift
  * If anything to do with data warehousing seen in the question, start considering Redshift to be part of the solution
  * Massive Parallel Processing (MPP) available for fast data aggregation, scoring and querying
  * Tight integration with SM
  * Dynamic data masking obfuscates sensitive data in specific columns in real-time, preserving source data integrity and avoiding data duplication or transformation.
  * Materialized views exclude sensitive fields but require creating and maintaining additional views and do not dynamically obfuscate data, which may not fully protect sensitive information.


# AWS Glue
  * serverless ETL service that uses Apache Spark under the hood and is suitable for scalable data transformations
  * can be used to apply custom masking transformations on sensitive fields in tabular data, preserving the dataset's structure and order for downstream use
  * glue partitioning aids parallel processing and boosts query performance
  * Glue DataBrew offers imputing missing values, standardized formatting, region specific cleaning rules, which ensures data quality before a model processes the input(s)
  * If wanting to optimize ETL costs (eg: avoid using more resources than necessary) decrease the number of Data Processing Units (DPUs) as the default might be more than what is required for a given job
  * Inputs:
    * Aurora
    * Postgres, Redshift, SqlServer, Oracle, MySql (JDBC datastores) (RDS based or otherwise)
    * Dynamodb
    * mongodb/documentdb
    * Kinesis Data Streams
    * Kafka/Amazon Managed Streaming for Apache Kafka
    * Athena
    * Spark
    * S3
    * Files (Orc, Parquet)
  * Outputs:
    * S3
    * JDBC (RDS, Redshift)
    * Glue Data Catalog
   
## AWS Glue Data Catalog
  * Central metadata repository storing schema definitions and table information for data across AWS analytics services.
  * supports tagging
  * IAM policies do not provide fine-grained access control for data at this level in Athena queries (look to Lake Formation for this sort of thing)

## SM Data Wrangler
  * Provide comprehensive data preparation and (prebuilt) transformations (eg: (cleaning normalizing, text tokenization)
  * Offers easy to use interactive, visual interface for data prep (e.g. cleaning transforming analyzing data) which is ideal for limited, low code use experience, but is not intended for large-scale distributed data processing across multiple heterogeneous data sources.
  * provides built-in transformations to mask sensitive data in tabular datasets while maintaining data integrity and structure.
  * Inputs
    * S3
    * Athena
    * Redshift
    * EMR
    * Lake formation (via Athena or AWS SDK awswrangler lib)
    * SM Feature Store
    * 3rd party sources (eg: Databricks, Snowflake Saas)
  * Outputs
    * S3
    * SM Processing
    * SM Pipelines
    * SM Feature Store
    * Autopilot
    * As a jupyter notebook
    * 3rd party external destinations
    * Amazon Personalize
    * Athena
    * Redshift
  * Does not integrate with DynamoDB

### SM Data Wrangler versus AWS Glue vs EMR
  * All are great for ETL
  * SM Data Wrangler more efficient when integrating with SM (eg: ETL=>SM Feature Store)
  * Glue and EMR are great for large-scale distributed data processing across multiple heterogeneous data sources, though EMR is best if full control over configurations and cluster management.
  * SageMaker Data Wrangler is optimized for interactive data preprocessing and visualization but is not intended for large-scale distributed data processing across multiple heterogeneous data sources.

# AWS Lake Formation
  * Managed service that simplifies the creation, security, and management of data lakes with fine-grained access control and centralized governance.
  * Can assign tags to datasets
  * Can define Lake Formation permissions based on those tags.
  * Assign analysts specific tags for their roles.

# Miscellaneous

## AWS Lex
  * Lex's speech recognition does not optimize fallback handling
  * Lex’s fallback intent ensures that ambiguous user queries are handled appropriately (eg: when Kendra doesn’t provide a clear match)

## AWS WAF
  * Designed to protect web applications at the application layer, HTTP/S (Layer 7)
  * Does not block network layer traffic within a VPC
  * Not suitable for blocking IP addresses at the subnet or network level.

## Network Access Control List (NACL)
  * Operates at the subnet level with explicit allow/deny rules - ideal for blocking specific IPs without disrupting legitimate traffic
  * Stateless - evaluates rules for both inbound and outbound traffic
  * Centralized control over multiple resources
  * Blocks malicious traffic at the subnet boundary
  * Best for fine-grained network-level filtering in VPC environments (eg: SM training jobs) while preserving access for authorized systems

## KMS
  * CMK provides full control over policies and grants, automated key rotation, and integrate with CloudTrail to record all cryptographic operations for auditing purposes
  * AWS managed keys (AWS owned or AWS-managed CMKs) do not allow custom key policies or rotation schedules
  * CloudTrail records all KMS API/operations for the sake of auditing (CloudWatch isn't designed for this)

## AWS Secrets Manager
  * Managed Rotation in AWS Secrets Manager is primarily designed for database credentials
  * Does not support automatic rotation of arbitrary API tokens, though it can securely store them
  * For API tokens, look to a Lambda to automate token rotation on a schedule (eg: every 90 days)

## EKS
  * managed kubernetes service that reduces operational overhead while providing full container orchestration
  * Horizontal Pod Autoscaler (HPA) automatically scales pod replicas based on real-time metrics per configuration (CPU, memory, etc.)
  * Managed control plane - no manual cluster management
  * Dynamic scaling based on observed workload metrics
  * Full kubernetes orchestration for containerized applications

## Fargate
  * serverless compute engine for containers
  * does not provide native Kubernetes orchestration features required for managing EKS workloads directly.

## Load Balancers
  * Need both port 443 and 80 to be open with the latter being redirected to the former if enabled by the attachment of an SSL certificate to the LB to allow the termination of HTTPS connections and thus serve secure content

## AWS Cost Explorer
  * A visualization tool for analyzing cost and usage trends over time, but it does not provide alerting capabilities.
  * provides insights but cannot send cost threshold alerts
  * provide visibility and recommendations but lack built-in alerting functionality

## AWS Budgets
  * A cost management service that allows users to set spending thresholds and receive automated alerts when actual or forecasted costs exceed those limits.
  * must be used to configure and send cost alerts, although it can use Cost Explorer data

## Amazon CloudWatch
  * while powerful for operational monitoring (CPU, memory, latency), is not designed to monitor or alert on billing data.

## AWS Trusted Advisor
  * A best-practice guidance tool that identifies cost optimization, security, and performance improvements, but it does not send budget alerts.
  * provide visibility and recommendations but lack built-in alerting functionality

## AWS Batch
  * Better matched over SM Batch jobs for extremely large, compute-intensive/high performance/scalable batch workloads 

## Catastrophic forgetting: 
  * when NNs abruptly lose previously learned information when trained on new, sequential data
  * Continual learning methods such as rehearsal or elastic weight consolidation can help model retention of previous knowledge

## Early Stopping
  * Stops training when validation metric degrades, preventing overfitting

## Feature selection versus model regularization
  * Model regularization does not directly select or remove input features
  * Model regularization reduces overfitting by penalizing model complexity
  * Feature selection systematically identifies and retains the most predictive features, while discarding irrelevant/redundant features to reduce model complexity to improve accuracy

## L1 (LASSO) vs L2 (Ridge) Regularization
  * Preventing overfitting in ML in general
  * A regularization term is added as weights are learned
  * L1 term is the sum of the absolute values of the weights as a penalty to the model's loss function
    * Performs feature selection - entire features go to 0
    * Computationally inefficient
    * Sparse output
    * Good to avoid curse of dimensionality
    * When to use L1
      * Feature selection can reduce dimensionality
      * Out of 100 features, maybe only 10 end up with non-zero coefficients!
      * The resulting sparsity can make up for its computational inefficiency
      * But, if you think all of your features are important, L2 is probably a better choice.
  * L2 term is the sum of the square of the weights
    * All features remain considered, just weighted
    * Computationally efficient
    * Dense output
  * Same idea can be applied to loss functions and/or weights as learned

## R^2 (the coefficient of determination)
  * Indicate how much variance in the target (dependent) variable is explained by the independent variables of the model

## Recall:
  * TP/(TP + FN) = TP/P
  * useful evaluation metric to reduce the risk of false negatives
  * precision and recall are the most appropriate metrics for tuning and monitoring a loan default model

## Accuracy:
  * (TP + TN)/(TP + FP + TN + FN)
  * not reliable in imbalanced datasets because it does not distinguish between false positives and false negatives
  * ratio of correct predictions, which may be misleading with imbalanced classes

## F1 Score: 
  * 2TP/(2TP + FP + FN) = 2 * (Precision * Recall)/(Precision+Recall)
  * useful to balance precision and recall, but both are more directly aligned with the target objective, true positives (eg: default/fraud/etc.).
  * harmonic mean of precision and recall—used when a balance between the two is needed.

## AUC/ROC: 
  * Useful metric for understanding performance across thresholds and imbalanced datasets. 
  * Does not directly capture the trade-off between false positives and false negatives
  * Measures a model’s ability to distinguish between classes by plotting true positive rate vs. false positive rate across thresholds.

## Precision:
  * TP/(TP + FP)
  * useful evaluation metric to reduce the risk of false positives
  * precision and recall are the most appropriate metrics for tuning and monitoring a loan default model

## Specificity:
  * TN/(TN + FP) = TN/N
  * useful evaluation metric to reduce the risk of false positives
  * Less relevant when primary concern is identifying True Positives and avoiding False Negatives (better suited for precision and recall)
  * The proportion of true negatives correctly identified—focuses on minimizing false positives in some contexts.

## SM Model Monitor
  * Model monitor does not provide experiment tracking (look to SM Experiments for this)
  * Evaluates the model’s performance in production by ingesting and merging actual outcomes (ground truth data) with model predictions and comparing predicted results against the observed outcomes.

## SM Model Monitor,  CloudWatch alerts, or SM built-in evaluation tools/SDK
  * continuously track precision and recall. If a drop in recall is detected, indicating increased financial risk, the pipeline can trigger a retraining step using updated customer behavior data.
  * SM provides built-in evaluation tools and allows users to plot training metrics (for users to visualize learning progress so as to adjust) using the SM SDK to assess the model’s performance before deployment.

# Model Overfitting
  * Compare training and validation loss curves over time: if validation loss much higher than training loss-> model overfitting

## AWS CodePipeline
  * fully managed continuous delivery (CD) service that automates software release processes (building/testing/deployment) for fast and reliable updates
  * does not offer automated quality checks on models

## AWS CodeBuild
  * a fully managed continuous integration service that compiles source code, runs tests, and produces ready-to-deploy software packages
  * utilizes Docker images that handles all dependencies/libraries for model training and testing
  * does not offer automated quality checks on models

## AWS CloudFormation
  * utilized to define CI/CD IaC for easy management, versioning and replication
  * When a CloudFormation stack is deleted, all resources defined within it are deleted

## Docker

## Athena
  * partition projection

## Blue/Green Deployments
  * Allows safe rollouts with instant rollback (provides HA) if problems encountered
  * Variants:
    * All at once: shift everything, monitor, terminate blue fleet
    * Canary: shift a small portion of traffic and monitor
    * Linear: Shift traffic in linearly spaced steps

## Weighted Traffic Splitting
  * Methodology of gradually routing traffic to different model versions so as to A/B test
  * Does not offer the same environmental isolation as that of Blue/Green Deployments

# EC2

## EC2 Autoscaling

### Scaling Policy

#### Scheduled Scaling
  * Works well for predictable traffice, but can't react to spikes or drops

#### Target Tracking Scaling
  * Continuously monitors metric(s) to adjust capacity up or down in accordance in real-time ensuring optimal performance
  * If maintaining low latency, track latency and request throughput (concurrency) to ensure low-latency predictions so as to autoscale and maintain availability to maintain optimal performance

## EC2 Pricing Options suitability

### Reserved Instances
  * Best suited for steady state workloads (prod)
  * Lack flexibility to handle unpredictable/varying trafflic load

## EC2 Type suitability
  * General note:
    * CPU-based instances are more cost-effective for development/testing purposes, but will have higher latency (eg: production usage)
    * GPU-based instances are less cost-effective for development/testing purposes, but will have lower latency (eg: production usage)

### G4DN (Nvidia T4 GPUs) 
  * provide modest power and cost savings but P3 or P4 is better for compute/low latency needs

### Inf1 
  * purposely built for high throughput, low latency inference

### M5
  * provide balanced resources, but lacks specialized GPU(s) necessary for efficient training of ML models

### P3 (Nvidia v100 GPUs)
  * offer powerful GPU that significantly reduces training time and improves computational performance for ML workload (eg: low latency inference)

### P4 (Nvidia A100 GPUs) 
  * offer massive compute/memory bandwidth

### R5
  * instances optimized for memory intensive applications, but lacks GPU(s), which is essential for efficient ML training

### T2
  * provides burst CPU performance, but not suitable for compute intensive tasks like ML model training, due to limited CPU and lack of GPU(s)

# Exploratory Data Analysis (EDA) 
  * used to understand data distributions
  * address missing values
  * assess the class imbalance before determining if an ML solution is feasible.
 
# Oversampling
  * should not be applied before conducting EDA to understand data quality, distribution (eg: class imbalance), and missing values.

# Ensemble Learning

## (Model) Stacking
  * Ensemble learning technique that combines more than one model through a meta-model that optimally weights/integrates the base learners to improve predictive performance at the expense of interpretability
  * Captures complementary information from the input models to result in more accurate/results

## Bagging
  * Trains multiple instances of the same algorithm on bootstrapped samples and averages these predictions to reduce variance (eg: Random Forest)

## Voting Ensemble
  * Simple aggregation technique where multiple models vote (greatest result for classification and average for regression) without learning optimal weights or relationships

# Shortcuts
  * 'manually' is usually a tell to not use the premise (eg: CPU/memory scaling doesn't necessarily help with manually scaled)
  * 'custom script' is a tell
