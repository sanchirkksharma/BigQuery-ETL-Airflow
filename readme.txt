** Global Health Data Pipeline (Airflow + BigQuery) **
#Overview
This project implements an end‑to‑end ELT pipeline on Google Cloud to securely ingest global health data and transform it into country‑specific datasets for analytics and reporting. Apache Airflow orchestrates the workflow, while Google BigQuery performs data processing and storage. The pipeline demonstrates core data engineering concepts including ingestion, orchestration, transformation, dependency management, and warehouse modeling.

## Architecture
Source → Storage → Orchestration → Warehouse → Transform 
Global CSV → GCS → Airflow → BigQuery (staging) → BigQuery (transform)

##Objectives
1. Load global health CSV data into BigQuery
2. Ensure pipeline runs only when source file exists
3. Transform dataset into country‑specific tables
4. Demonstrate Airflow orchestration patterns
5. Build scalable ELT architecture on GCP

##Tech Stack
1. Cloud: Google Cloud Platform (GCP)
2. Storage: Google Cloud Storage (GCS)
3. Warehouse: BigQuery
4. Orchestration: Apache Airflow (VM‑hosted)
5. Language: Python

## Data Layers
1. Staging Layer
Dataset: staging_dataset -> Raw data loaded from CSV
Single global table: global_data
Purpose: source of truth

2. Transform Layer
Dataset: transform_dataset -> Country‑specific tables created from staging:
usa_table, india_table, germany_table, japan_table, france_table, canada_table, italy_table
Purpose: segmented analytics data

## DAG — Load and Transform
Full ELT workflow.
Flow: Check file → Load staging → Create country tables
Operators:
1. GCSObjectExistenceSensor
2. GCSToBigQueryOperator
3. BigQueryInsertJobOperator

## Running the Pipeline
1. Start Airflow on VM: 
        nohup airflow standalone > airflow.log 2>&1 &
2. Open UI:
        http://<VM-IP>:8080
3. Trigger DAG:
        load_and_transform

## Conclusion
This project demonstrates a production‑style cloud data pipeline using Airflow and BigQuery, implementing ingestion, orchestration, and transformation for secure country‑level analytics on global health data.