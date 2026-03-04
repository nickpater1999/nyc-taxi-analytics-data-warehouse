# NYC Taxi Analytics Data Warehouse

A PostgreSQL-based analytical data model built from raw NYC Yellow Taxi trip records.

This project demonstrates schema inspection, data standardization, dimensional modeling, and advanced SQL analytics using a star schema architecture.

---

## Overview

This project builds a structured analytical data warehouse from raw 2023 NYC Yellow Taxi trip data. The source data consists of 12 monthly parquet files containing millions of trip-level transactions collected by the Taxi and Limousine Commission (TLC) and published via [NYC Open Data](https://data.cityofnewyork.us/Transportation/2023-Yellow-Taxi-Trip-Data/4b4i-vvec/about_data).

The objective of this project is to transform raw, partitioned trip data into a clean, relational model suitable for analytics and reporting. The final system supports time-series analysis, dimensional reporting, and advanced SQL-based KPI development.

### Architecture Overview

The pipeline follows a layered warehouse approach:

Raw parquet files
→ Canonical Schema Enforcement (Python)
→ PostgreSQL Raw Table
→ SQL Staging Layer (Data Cleaning & Validation)
→ Dimensional Model (Star Schema)
→ Analytical Query Layer

### Tools Used

- PostgreSQL (data modeling and analytics)
- Python (schema inspection and ingestion)
- SQL (staging, modeling, analytics)

### Skills Demonstrated

- Schema drift detection
- Canonical schema design
- Relational modeling
- Star schema construction
- Primary and foreign key constraints
- Indexing strategy
- Window functions and advanced SQL analytics

### Status

Active development.

Sections are incrementally refined and merged into `main` upon reaching stable milestones.

---

## 1. Data Collection

The 2023 Yellow Taxi Trip dataset was selected from [NYC Open Data](https://data.cityofnewyork.us/Transportation/2023-Yellow-Taxi-Trip-Data/4b4i-vvec/about_data).
- Dataset: 2023 Yellow Taxi Trip Data
- Source: New York City Taxi and Limousine Commission
- Format: 12 monthly parquet files
- Scope: Trip-level transactional data including timestamps, fares, distances, and coded identifiers

External links:
- [2023 Yellow Taxi Trip Data](https://data.cityofnewyork.us/Transportation/2023-Yellow-Taxi-Trip-Data/4b4i-vvec/about_data)
- [About TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

---

## 2. Schema Inspection

The 12 monthly parquet files were inspected using Python to identify:
- Column name inconsistencies
- Datatype mismatches
- Naming variations (e.g., `airport_fee` vs `Airport_fee`)
- Integer size inconsistencies across partitions

A canonical schema was defined to enforce consistency prior to ingestion into PostgreSQL.

---

## 3. Data Standardization

Column names were standardized to `lowercase snake_case`.

Datatype alignment was enforced to ensure consistent loading into PostgreSQL. Only structural normalization was performed at this stage; business logic validation was deferred to the SQL staging layer.

---

## 4. Raw Layer Construction

A `raw_trips` table was created in PostgreSQL to store the ingested data without transformation.

This layer preserves original values and serves as the immutable source for downstream modeling.

---

## 5. Staging & Data Cleaning

A `stg_trips` staging table was created using SQL to:
- Remove invalid trip records
- Enforce logical timestamp order
- Filter negative monetary values
- Cast fields to final modeling datatypes

Data cleaning was intentionally performed in SQL to demonstrate database-layer transformation capability.

---

## 6. Dimensional Modeling

A star schema was designed consisting of:
- `dim_date`
- `dim_location`
- `dim_vendor`
- `dim_ratecode`
- `dim_payment_type`
- `fact_trips`

Foreign key constraints were implemented to enforce referential integrity.

Indexes were added to optimize query performance.

---

## 7. Analytical Layer

TODO: this section

The final model supports analytical queries including:

Key Business Questions:
- What are monthly revenue trends?
- Which pickup zones generate the highest fare revenue?
- What are peak trip hours by borough?

Advanced SQL Features Demonstrated
- Window functions (`ROW_NUMBER`, `RANK`, `LOG`)
- Rolling averages
- Partitioning aggregations
- Time-based grouping
- KPI calculations

---

## Future Improvements

- Integration with Looker Studio for dashboard visualization
- Partitioning strategy for large-scale performance optimization
- Incremental loading framework
- Additional year-over-year analysis
