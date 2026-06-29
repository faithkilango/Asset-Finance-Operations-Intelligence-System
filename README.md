# Asset-Finance Operations Intelligence System

An end-to-end business intelligence case study that transforms fragmented operational, customer, repayment, asset and maintenance data into a structured PostgreSQL database, automated reconciliation workflow, risk-monitoring framework and Power BI management dashboard.

> **Portfolio disclosure:** This is an independent and anonymized portfolio case study inspired by common challenges in asset-finance and mobility operations. All organisations, names, identifiers, financial values and records used in the public project are fictional, anonymized or synthetically generated.

## Project Status

🚧 **In Progress**

## Business Problem

An asset-finance and rent-to-own mobility business manages riders, financed assets, weekly earnings, repayments, maintenance charges and payouts across disconnected spreadsheets and operational systems.

This makes it difficult for management to obtain a consistent view of:

* expected versus actual collections
* customer outstanding balances
* payout calculations
* asset utilization
* maintenance and downtime
* high-risk accounts
* reconciliation and data-quality exceptions

## Project Objective

Build a reliable business intelligence solution that:

1. Structures fragmented operational data.
2. Cleans and validates source records.
3. Centralizes reporting data in PostgreSQL.
4. automates weekly repayment and payout calculations.
5. Identifies reconciliation exceptions.
6. Monitors fleet and customer risk.
7. Presents decision-ready management KPIs in Power BI.

## Business Value
The solution is designed to help management:
1. Improve visibility into collections and outstanding balances
2. Reduce manual reconciliation work
3. Detect data-quality problems earlier
4. Identify high-risk customer accounts
5. Monitor asset utilization and downtime
6. Prioritize operational and collection interventions
7. Make faster and more consistent decisions 

## Planned Solution Architecture

```text
Synthetic source files
        ↓
Python cleaning and validation
        ↓
PostgreSQL database
        ↓
SQL business logic and reporting views
        ↓
Power BI dashboard
        ↓
Management insights and actions
```

## Planned Dashboard Pages

1. Executive Overview
2. Collections and Reconciliation
3. Fleet and Maintenance
4. Risk and Intervention

## Tools

* PostgreSQL
* SQL
* Python
* pandas
* Power BI
* Excel
* GitHub

## Planned Repository Structure

asset-finance-operations-intelligence/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── data/
│   ├── sample/
│   └── processed/
│
├── docs/
│   ├── project_scope.md
│   ├── business_requirements.md
│   ├── business_questions.md
│   ├── kpi_dictionary.md
│   ├── data_model.md
│   └── findings_and_recommendations.md
│
├── python/
│   ├── generate_sample_data.py
│   ├── data_cleaning.py
│   └── data_validation.py
│
├── sql/
│   ├── 01_create_schema.sql
│   ├── 02_create_tables.sql
│   ├── 03_create_constraints.sql
│   ├── 04_data_quality_checks.sql
│   ├── 05_business_logic.sql
│   ├── 06_kpi_queries.sql
│   └── 07_reporting_views.sql
│
├── dashboard/
│   └── screenshots/
│
└── images/
