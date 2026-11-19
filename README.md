# Enterprise Omnichannel & IoT Telemetry Lakehouse

An end-to-end **Bronze–Silver–Gold Medallion Lakehouse** architecture combining batch operational feeds and real-time event telemetry into reliable analytics and ML-ready datasets using **PySpark**, **Spark SQL**, **Python**, and **Azure Data / Lakehouse patterns**.

## Architecture Overview
- **Bronze Layer (Raw Immutable):** Ingests batch feeds and real-time event streams (e.g., Event Hubs / ADLS Gen2) with ingestion metadata (`ingested_at`, `source_system`, `batch_id`) without mutating raw payloads.
- **Silver Layer (Cleaned, Validated & Deduplicated):** Enforces schemas, handles late/out-of-order records, deduplicates via deterministic keys/windowing, and routes malformed or invalid records to a quarantine path.
- **Gold Layer (Curated Analytics & ML Marts):** Produces business-ready dimensional/fact tables and aggregated metrics for downstream reporting and machine learning.

## Key Engineering Highlights
- **Idempotent & Replayable Processing:** Designed around deterministic keys and partitioned storage so reruns do not corrupt downstream tables.
- **Data Quality & Quarantine:** Separates valid records from schema/value violations so upstream spikes or bad payloads do not fail Gold consumption.
- **Analytical & ML Readiness:** Structures curated tables for fast querying and feature generation.

## Repository Structure
- `spark_jobs/` — PySpark transformation stages (`bronze`, `silver`, `gold`)
- `sql/` — Table definitions and analytical queries
- `config/` — Pipeline configuration parameters
- `sample_data/` — Sample batch and telemetry records for local testing

## How to Run (Local / Spark / Databricks)
1. Clone the repository:
   ```bash
   git clone [https://github.com/imdhilipkumar/enterprise-omnichannel-iot-lakehouse.git](https://github.com/imdhilipkumar/enterprise-omnichannel-iot-lakehouse.git)
   cd enterprise-omnichannel-iot-lakehouse
