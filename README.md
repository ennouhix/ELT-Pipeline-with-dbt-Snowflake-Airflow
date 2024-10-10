
# ELT Pipeline with Snowflake, DBT, and Airflow

## Project Overview

This project builds an ELT pipeline using **Snowflake**, **DBT**, and **Airflow**. The process includes:
- Extracting data, loading it into Snowflake, and transforming it using DBT.
- Orchestrating the pipeline with Airflow.

## Tools Used

- **Snowflake**: Cloud data warehouse for storing data.
- **DBT**: For transforming data in Snowflake using modular SQL.
- **Airflow**: Orchestrates the ELT pipeline.

## ELT Process

### 1. Set Up Snowflake

Create a warehouse, database, and role:
```sql
CREATE WAREHOUSE DBT_Warehouse;
CREATE DATABASE DBT_Database;
CREATE ROLE DBT_Role;
GRANT USAGE ON WAREHOUSE DBT_Warehouse TO ROLE DBT_Role;
```

### 2. Configure DBT

Initialize DBT project and configure Snowflake in `dbt_project.yml`:
```bash
pip install dbt-core
dbt init project_name
```

### 3. Transform Data

Create source and staging models in DBT, e.g., `models/staging/stg_tpch_orders.sql`:
```sql
select
    o_orderkey as order_key,
    o_custkey as customer_key,
    o_totalprice as total_price
from
    {{ source('tpch', 'orders') }}
```

### 4. Orchestrate with Airflow

Use Airflow to schedule and manage the ELT pipeline. Airflow can trigger DBT models as DAGs to ensure efficient pipeline execution.

## Conclusion

This project showcases how to build a scalable and efficient ELT pipeline with modern cloud tools.
