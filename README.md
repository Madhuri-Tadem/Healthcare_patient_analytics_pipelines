# Healthcare_patient_analytics_pipelines

## Project Overview

The **Healthcare Patient Analytics Pipeline** is an end-to-end data engineering pipeline designed to process patient health records and generate analytics-ready datasets for healthcare analysis.

The pipeline ingests patient data from **AWS S3**, processes it using **Databricks and PySpark**, and stores it in **Delta Lake tables** following the **Medallion Architecture (Bronze, Silver, Gold layers)**.

The final output provides **aggregated healthcare metrics and patient risk scores** that can support predictive healthcare analytics and decision-making.

---

# Architecture

The pipeline follows the **Medallion Data Architecture**:

```
Raw Data (S3 CSV)
        │
        ▼
Bronze Layer
health_catalog.raw.patient_records
        │
        ▼
Silver Layer
health_catalog.processed.patient_cleaned
        │
        ▼
Gold Layer
health_catalog.analytics.health_metrics
```

Each layer progressively improves data quality and prepares the dataset for analytics.

---

# Data Source

**Dataset:** Heart Disease Dataset (Kaggle)

The dataset contains patient health information including:

* Age
* Blood pressure
* Cholesterol levels
* Heart rate
* Medical conditions
* Diagnosis indicators

Raw files are stored in:

```
s3://bucket/raw/health_records/YYYY/MM/DD/
```

---

# Pipeline Workflow

## 1. Data Ingestion (Bronze Layer)

Raw CSV files are ingested from **AWS S3** into Delta Lake tables.

Tasks performed:

* Read CSV files from S3
* Infer schema automatically
* Handle malformed records
* Partition data by year and month
* Store raw data in Delta format

Destination table:

```
health_catalog.raw.patient_records
```

---

# 2. Data Cleaning & Transformation (Silver Layer)

The Silver layer focuses on **data standardization and quality improvement**.

Transformations include:

* Removing duplicate records
* Standardizing date formats
* Cleaning missing or invalid values
* Standardizing medical codes
* Joining with dimension tables (e.g., hospitals)
* Preparing structured datasets for analytics

Destination table:

```
health_catalog.processed.patient_cleaned
```

---

# 3. Analytics & Risk Modeling (Gold Layer)

The Gold layer produces **analytics-ready datasets and healthcare metrics**.

Key operations:

* Compute patient heart disease risk scores
* Categorize patients into risk levels
* Aggregate patient health metrics
* Generate hospital performance indicators
* Produce regional disease trends

Destination table:

```
health_catalog.analytics.health_metrics
```

---

# Risk Scoring Logic

The pipeline calculates **patient heart disease risk scores** using key health indicators:

* Age
* Blood pressure
* Cholesterol
* Heart rate
* Existing medical conditions

Patients are categorized into:

* Low Risk
* Medium Risk
* High Risk

These metrics support **predictive healthcare analytics and risk assessment**.

---

# Pipeline Orchestration

The pipeline is orchestrated using **Databricks Workflows**.

Schedule:

```
Daily batch job
2:00 AM UTC
```

The workflow performs:

1. Data ingestion
2. Data transformation
3. Data aggregation
4. Data quality validation

---

# Error Handling & Monitoring

To ensure reliability, the pipeline includes:

* Logging of ETL errors
* Data quality checks
* Email alerts for anomalies

Error logs are stored in:

```
health_catalog.logs.etl_errors
```

---

# Performance Optimization

To improve efficiency and scalability, the pipeline uses:

* Delta Lake optimizations
* Table partitioning
* Data compaction
* Periodic vacuum operations

These optimizations improve query performance for large healthcare datasets.

---

# Testing

Pipeline testing includes:

* Unit tests for transformation logic
* Schema validation
* Record count validation
* Testing using Kaggle sample data

Testing is implemented using:

```
pytest
```

---

# Technology Stack

* Databricks
* PySpark
* Delta Lake
* AWS S3
* boto3
* pytest
* Git / GitHub

---

# Project Outcomes

This project demonstrates the implementation of a **production-style healthcare data pipeline**.

Key outcomes include:

* Scalable healthcare data pipeline using **Delta Lake and AWS S3**
* Reliable data processing with **data quality checks and error handling**
* Optimized query performance using **partitioning and Delta optimizations**
* Version-controlled development using **Git integration**
* Generation of **patient risk analytics for healthcare insights**

---

# Future Improvements

Potential enhancements include:

* Real-time patient data streaming
* Machine learning models for predictive healthcare analytics
* Integration with healthcare dashboards (Power BI / Tableau)
* Automated data validation frameworks

---

# Repository Structure

```
healthcare-patient-analytics-pipeline
│
├── ingestion
│   └── bronze_ingestion.py
│
├── transformations
│   └── silver_transformations.py
│
├── analytics
│   └── gold_metrics.py
│
├── tests
│   └── pipeline_tests.py
│
└── README.md
```

---

# Author

Madhuri Tadem
Data Engineering Project – Healthcare Analytics Pipeline
