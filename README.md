# dbt Fundamentals – Analytics Engineering Project (Postgres)

## Overview
This repository contains an end-to-end **analytics engineering project built with dbt Core**, completed as part of the **dbt Fundamentals Certificate** and adapted to run on a **local PostgreSQL warehouse**.

The project demonstrates how to design, test, document, and deploy analytics models using modern dbt best practices, including environment separation, version control, and production deployment workflows.

---

## Tech Stack
- **dbt Core**
- **PostgreSQL** (local warehouse)
- **SQL**
- **YAML**
- **Git & GitHub**

---

## Project Architecture

The project follows a layered analytics engineering design:

raw database
├── raw schema (source data)
├── dbt_dev schema (development environment)
└── analytics schema (production environment)


### Layers
- **Sources**
  - Raw data defined using dbt `sources`
  - Data provided via CSV-based seeds for learning purposes

- **Staging Layer**
  - Standardized and cleaned source data
  - Renamed columns, type consistency, and business-friendly naming
  - One staging model per source table

- **Marts Layer**
  - **Marketing mart**
    - `dim_customers`
  - **Finance mart**
    - `fct_orders`
  - Models designed for analytics and reporting use cases

---

## Data Quality & Testing

The project includes a comprehensive testing strategy:

- `not_null` tests
- `unique` tests
- `accepted_values` tests
- `relationships` tests
- Custom SQL data test to validate business logic

Tests are executed automatically as part of:

```bash
dbt build
```

---

## Documentation

This project includes comprehensive documentation maintained directly alongside the codebase to ensure clarity, discoverability, and long-term maintainability.

### What is documented
- **Source-level documentation**  
  Descriptions of raw source tables and their role in the analytics pipeline.
- **Model-level documentation**  
  Clear explanations of each staging and mart model, including business purpose.
- **Column-level descriptions**  
  Definitions for key columns to ensure shared understanding across stakeholders.
- **Markdown documentation files**  
  Additional `.md` files for staging models to provide richer context and explanations.

Keeping documentation close to the transformations ensures it stays up to date as the project evolves.

---

## Environments & Deployment

Two environments are configured using dbt targets to separate development from production.

### Development Environment
- **Schema**: `dbt_dev`
- Used for iterative development, experimentation, and feature work
- All new models and changes are developed and tested here first

### Production Environment
- **Schema**: `analytics`
- Deployment is executed **only from the `main` branch**
- Represents production-ready, analytics-consumable data models

### Deployment Command

```bash
dbt build --target prod
```
This command builds models, runs tests, and validates data quality as part of the production deployment.

---

## Note on Warehouse Choice

This project uses **PostgreSQL** instead of Snowflake or other cloud data warehouses.

PostgreSQL does **not support cross-database references**, so development and production environments are separated using **schemas within the same database** rather than separate databases.

In cloud data warehouses (e.g. **Snowflake**, **BigQuery**, **Redshift**), this separation would typically be implemented using **separate databases** for raw, development, and analytics layers.

This design choice reflects an awareness of **warehouse-specific constraints** while still adhering to analytics engineering best practices.

---

## Version Control Workflow

A professional Git workflow is used throughout the project:

- Feature-based Git branches for isolated development
- Incremental commits per topic (models, tests, documentation)
- All feature branches merged into `main` prior to production deployment
- Clean, traceable Git history that reflects real-world team workflows

---

## Notes on Seeds

CSV files in the `seeds/` directory are used as **demo source data** for learning and development purposes.

In real production systems:

- Source data is typically loaded by ingestion tools (e.g. **Fivetran**, **Airbyte**, CDC pipelines)
- dbt is used **only for transforming existing warehouse tables**
- dbt seeds are generally limited to small reference or lookup datasets

Seeds in this project simulate upstream source systems to enable a **fully self-contained learning workflow**.

---

## What This Project Demonstrates

This project showcases:

- Analytics engineering best practices
- dbt project structure and modeling conventions
- Automated data quality testing
- Environment separation and deployment workflows
- Awareness of warehouse-specific constraints
- Professional Git usage for analytics projects

---

## Author

Built by **Balazs Illovai** as part of a transition toward more technical analytics and data engineering roles.

