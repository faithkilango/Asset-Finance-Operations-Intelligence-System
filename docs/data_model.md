# Data Model

## Purpose

This document defines the planned relational data model for the Asset-Finance Operations Intelligence System.

The model is designed to support:

* Rider onboarding
* Asset management
* Rent-to-own contracts
* Asset assignments
* Weekly earnings
* Repayments
* Operational charges
* Maintenance tracking
* Weekly rider statements
* Reconciliation
* Risk monitoring
* Power BI reporting

## Data Model Principles

The database will follow these principles:

* Each major business entity will have its own table.
* Each record will have a unique identifier.
* Relationships will be enforced through foreign keys.
* Transactional data will be stored separately from master data.
* Historical changes will be preserved where possible.
* Reporting views will be created separately from operational tables.
* Synthetic data will be used throughout the public project.

## Core Tables

### 1. `riders`

Stores the master record for each rider.

| Column          | Data Type | Description                                                | Key         |
| --------------- | --------- | ---------------------------------------------------------- | ----------- |
| rider_id        | VARCHAR   | Unique rider identifier                                    | Primary Key |
| first_name      | VARCHAR   | Fictional rider first name                                 |             |
| last_name       | VARCHAR   | Fictional rider last name                                  |             |
| onboarding_date | DATE      | Date the rider joined                                      |             |
| rider_status    | VARCHAR   | Active, inactive, suspended, exited or ownership-completed |             |
| region          | VARCHAR   | Rider operating region                                     |             |
| platform        | VARCHAR   | Delivery or mobility platform                              |             |
| created_at      | TIMESTAMP | Record creation timestamp                                  |             |
| updated_at      | TIMESTAMP | Last update timestamp                                      |             |

### 2. `assets`

Stores the master record for each financed asset.

| Column           | Data Type | Description                                                   | Key         |
| ---------------- | --------- | ------------------------------------------------------------- | ----------- |
| asset_id         | VARCHAR   | Unique asset identifier                                       | Primary Key |
| asset_type       | VARCHAR   | Type of asset                                                 |             |
| asset_model      | VARCHAR   | Asset model                                                   |             |
| acquisition_date | DATE      | Date the asset was acquired                                   |             |
| acquisition_cost | NUMERIC   | Cost of acquiring the asset                                   |             |
| current_status   | VARCHAR   | Active, idle, maintenance, repossessed or ownership-completed |             |
| current_location | VARCHAR   | Current operating location                                    |             |
| created_at       | TIMESTAMP | Record creation timestamp                                     |             |
| updated_at       | TIMESTAMP | Last update timestamp                                         |             |

### 3. `contracts`

Stores the rent-to-own contract between a rider and an asset.

| Column                  | Data Type | Description                                | Key         |
| ----------------------- | --------- | ------------------------------------------ | ----------- |
| contract_id             | VARCHAR   | Unique contract identifier                 | Primary Key |
| rider_id                | VARCHAR   | Rider linked to the contract               | Foreign Key |
| asset_id                | VARCHAR   | Asset linked to the contract               | Foreign Key |
| contract_start_date     | DATE      | Contract start date                        |             |
| contract_end_date       | DATE      | Planned contract end date                  |             |
| weekly_repayment_amount | NUMERIC   | Contractual weekly repayment               |             |
| deposit_amount          | NUMERIC   | Initial deposit paid                       |             |
| total_contract_value    | NUMERIC   | Total amount due under the contract        |             |
| total_contract_weeks    | INTEGER   | Planned contract duration                  |             |
| contract_status         | VARCHAR   | Active, suspended, terminated or completed |             |
| created_at              | TIMESTAMP | Record creation timestamp                  |             |
| updated_at              | TIMESTAMP | Last update timestamp                      |             |

### 4. `asset_assignments`

Stores the history of asset assignments to riders.

| Column                | Data Type | Description                                       | Key         |
| --------------------- | --------- | ------------------------------------------------- | ----------- |
| assignment_id         | VARCHAR   | Unique assignment identifier                      | Primary Key |
| rider_id              | VARCHAR   | Assigned rider                                    | Foreign Key |
| asset_id              | VARCHAR   | Assigned asset                                    | Foreign Key |
| assignment_start_date | DATE      | Assignment start date                             |             |
| assignment_end_date   | DATE      | Assignment end date                               |             |
| assignment_status     | VARCHAR   | Active or closed                                  |             |
| assignment_reason     | VARCHAR   | New assignment, replacement, repossession or exit |             |
| created_at            | TIMESTAMP | Record creation timestamp                         |             |

### 5. `weekly_earnings`

Stores rider earnings by reporting week.

| Column           | Data Type | Description                            | Key         |
| ---------------- | --------- | -------------------------------------- | ----------- |
| earning_id       | VARCHAR   | Unique earning record identifier       | Primary Key |
| rider_id         | VARCHAR   | Rider linked to the earning            | Foreign Key |
| week_start_date  | DATE      | Start date of the reporting week       |             |
| week_end_date    | DATE      | End date of the reporting week         |             |
| gross_earnings   | NUMERIC   | Total rider earnings before deductions |             |
| platform         | VARCHAR   | Source platform                        |             |
| source_reference | VARCHAR   | Source file or statement reference     |             |
| created_at       | TIMESTAMP | Record creation timestamp              |             |

### 6. `payments`

Stores payments made or recovered against rider obligations.

| Column            | Data Type | Description                                | Key         |
| ----------------- | --------- | ------------------------------------------ | ----------- |
| payment_id        | VARCHAR   | Unique payment identifier                  | Primary Key |
| rider_id          | VARCHAR   | Rider linked to the payment                | Foreign Key |
| contract_id       | VARCHAR   | Related contract                           | Foreign Key |
| payment_date      | DATE      | Payment date                               |             |
| payment_amount    | NUMERIC   | Amount paid                                |             |
| payment_type      | VARCHAR   | Repayment, deposit, recovery or adjustment |             |
| payment_reference | VARCHAR   | Unique payment reference                   | Unique      |
| payment_status    | VARCHAR   | Successful, pending, reversed or failed    |             |
| created_at        | TIMESTAMP | Record creation timestamp                  |             |

### 7. `operational_charges`

Stores approved non-repayment charges applied to riders.

| Column           | Data Type | Description                                       | Key         |
| ---------------- | --------- | ------------------------------------------------- | ----------- |
| charge_id        | VARCHAR   | Unique charge identifier                          | Primary Key |
| rider_id         | VARCHAR   | Rider linked to the charge                        | Foreign Key |
| asset_id         | VARCHAR   | Related asset, where applicable                   | Foreign Key |
| charge_date      | DATE      | Date the charge was applied                       |             |
| charge_type      | VARCHAR   | Maintenance, battery, insurance, penalty or other |             |
| charge_amount    | NUMERIC   | Charge value                                      |             |
| charge_status    | VARCHAR   | Approved, pending, reversed or rejected           |             |
| source_reference | VARCHAR   | Source record reference                           |             |
| created_at       | TIMESTAMP | Record creation timestamp                         |             |

### 8. `maintenance_records`

Stores maintenance incidents and related costs.

| Column                 | Data Type | Description                                    | Key         |
| ---------------------- | --------- | ---------------------------------------------- | ----------- |
| maintenance_id         | VARCHAR   | Unique maintenance identifier                  | Primary Key |
| asset_id               | VARCHAR   | Asset under maintenance                        | Foreign Key |
| rider_id               | VARCHAR   | Rider assigned at the time, where applicable   | Foreign Key |
| maintenance_start_date | DATE      | Maintenance start date                         |             |
| maintenance_end_date   | DATE      | Maintenance completion date                    |             |
| maintenance_type       | VARCHAR   | Preventive, corrective, accident or inspection |             |
| maintenance_category   | VARCHAR   | Mechanical, electrical, battery, tyre or other |             |
| maintenance_cost       | NUMERIC   | Total maintenance cost                         |             |
| downtime_days          | INTEGER   | Number of unavailable days                     |             |
| maintenance_status     | VARCHAR   | Open, in progress, completed or cancelled      |             |
| created_at             | TIMESTAMP | Record creation timestamp                      |             |

### 9. `weekly_statements`

Stores the calculated weekly rider financial position.

| Column                  | Data Type | Description                                       | Key         |
| ----------------------- | --------- | ------------------------------------------------- | ----------- |
| statement_id            | VARCHAR   | Unique statement identifier                       | Primary Key |
| rider_id                | VARCHAR   | Rider linked to the statement                     | Foreign Key |
| contract_id             | VARCHAR   | Contract linked to the statement                  | Foreign Key |
| week_start_date         | DATE      | Start of reporting week                           |             |
| gross_earnings          | NUMERIC   | Rider earnings before deductions                  |             |
| previous_balance        | NUMERIC   | Balance carried from the previous week            |             |
| expected_repayment      | NUMERIC   | Repayment due for the current week                |             |
| actual_repayment        | NUMERIC   | Repayment recovered during the week               |             |
| maintenance_deduction   | NUMERIC   | Maintenance amount deducted                       |             |
| other_charges           | NUMERIC   | Other approved charges                            |             |
| total_deductions        | NUMERIC   | Total amount deducted                             |             |
| calculated_payout       | NUMERIC   | Expected payout after deductions                  |             |
| recorded_payout         | NUMERIC   | Payout recorded in the source system              |             |
| reconciliation_variance | NUMERIC   | Difference between calculated and recorded payout |             |
| closing_balance         | NUMERIC   | Balance carried to the next week                  |             |
| risk_level              | VARCHAR   | Low, medium, high or critical                     |             |
| created_at              | TIMESTAMP | Record creation timestamp                         |             |

### 10. `risk_assessments`

Stores weekly rider-risk classifications and reasons.

| Column                 | Data Type | Description                       | Key         |
| ---------------------- | --------- | --------------------------------- | ----------- |
| risk_assessment_id     | VARCHAR   | Unique risk assessment identifier | Primary Key |
| rider_id               | VARCHAR   | Rider being assessed              | Foreign Key |
| assessment_date        | DATE      | Risk assessment date              |             |
| missed_payment_score   | INTEGER   | Score for missed repayments       |             |
| debt_trend_score       | INTEGER   | Score for increasing debt         |             |
| earnings_decline_score | INTEGER   | Score for declining earnings      |             |
| inactivity_score       | INTEGER   | Score for prolonged inactivity    |             |
| maintenance_score      | INTEGER   | Score for repeated maintenance    |             |
| total_risk_score       | INTEGER   | Total weighted score              |             |
| risk_level             | VARCHAR   | Low, medium, high or critical     |             |
| primary_risk_reason    | VARCHAR   | Main reason for classification    |             |
| recommended_action     | VARCHAR   | Suggested intervention            |             |
| created_at             | TIMESTAMP | Record creation timestamp         |             |

### 11. `interventions`

Stores follow-up actions assigned to rider accounts.

| Column              | Data Type | Description                                                | Key         |
| ------------------- | --------- | ---------------------------------------------------------- | ----------- |
| intervention_id     | VARCHAR   | Unique intervention identifier                             | Primary Key |
| rider_id            | VARCHAR   | Rider requiring intervention                               | Foreign Key |
| risk_assessment_id  | VARCHAR   | Related risk assessment                                    | Foreign Key |
| intervention_date   | DATE      | Date the action was assigned                               |             |
| intervention_type   | VARCHAR   | Call, warning, payment plan, field follow-up or escalation |             |
| intervention_status | VARCHAR   | Open, in progress, completed or cancelled                  |             |
| assigned_team       | VARCHAR   | Team responsible for the action                            |             |
| completion_date     | DATE      | Date the action was completed                              |             |
| outcome             | VARCHAR   | Result of the intervention                                 |             |
| created_at          | TIMESTAMP | Record creation timestamp                                  |             |

### 12. `data_quality_issues`

Stores records that fail data-quality or validation rules.

| Column            | Data Type | Description                                            | Key         |
| ----------------- | --------- | ------------------------------------------------------ | ----------- |
| issue_id          | VARCHAR   | Unique issue identifier                                | Primary Key |
| source_table      | VARCHAR   | Table or file where the issue was found                |             |
| source_record_id  | VARCHAR   | Identifier of the affected record                      |             |
| issue_type        | VARCHAR   | Missing, duplicate, invalid, unmatched or inconsistent |             |
| issue_description | VARCHAR   | Description of the problem                             |             |
| issue_status      | VARCHAR   | Corrected, rejected or manual review                   |             |
| detected_at       | TIMESTAMP | Date and time of detection                             |             |
| resolved_at       | TIMESTAMP | Date and time of resolution                            |             |

## Table Relationships

The main relationships are:

* One rider can have one or more contracts over time.
* One asset can appear in one or more contracts over time.
* One rider can have many weekly earnings records.
* One rider can have many payments.
* One rider can have many operational charges.
* One asset can have many maintenance records.
* One rider can have many weekly statements.
* One rider can have many risk assessments.
* One risk assessment can have one or more interventions.
* One rider can have multiple asset assignments over time.
* One asset can have multiple assignments over time, but only one active assignment at a time.

## Relationship Summary

```text
riders
  ├── contracts
  ├── asset_assignments
  ├── weekly_earnings
  ├── payments
  ├── operational_charges
  ├── weekly_statements
  ├── risk_assessments
  └── interventions

assets
  ├── contracts
  ├── asset_assignments
  ├── operational_charges
  └── maintenance_records

contracts
  ├── payments
  └── weekly_statements

risk_assessments
  └── interventions
```

## Primary Keys

Each table will have a unique primary key:

* `rider_id`
* `asset_id`
* `contract_id`
* `assignment_id`
* `earning_id`
* `payment_id`
* `charge_id`
* `maintenance_id`
* `statement_id`
* `risk_assessment_id`
* `intervention_id`
* `issue_id`

## Foreign Keys

The database will use foreign keys to enforce relationships between:

* Riders and contracts
* Assets and contracts
* Riders and asset assignments
* Assets and asset assignments
* Riders and earnings
* Riders and payments
* Contracts and payments
* Riders and operational charges
* Assets and operational charges
* Assets and maintenance records
* Riders and maintenance records
* Riders and weekly statements
* Contracts and weekly statements
* Riders and risk assessments
* Riders and interventions
* Risk assessments and interventions

## Planned Constraints

The SQL database will include controls such as:

* Unique rider IDs
* Unique asset IDs
* Unique contract IDs
* Unique payment references
* Required fields for core records
* Positive financial values where applicable
* Valid status values
* Valid contract dates
* No maintenance end date before maintenance start date
* No assignment end date before assignment start date
* One active assignment per asset
* No payment linked to an unknown rider or contract
* No maintenance record linked to an unknown asset

## Reporting Views

The database will later create reporting views such as:

* `vw_weekly_collection_performance`
* `vw_rider_balances`
* `vw_reconciliation_exceptions`
* `vw_asset_status_summary`
* `vw_fleet_utilization`
* `vw_maintenance_performance`
* `vw_rider_risk`
* `vw_management_overview`

These views will provide clean, analysis-ready data for Power BI.

## Data Model Validation

Before implementation, the model should be checked to confirm that:

1. Every business requirement is supported by at least one table.
2. Every KPI has the required source fields.
3. Every relationship has a valid primary and foreign key.
4. Historical assignments and statuses can be preserved.
5. Weekly statements can be reproduced from source transactions.
6. Reconciliation calculations can be traced to source records.
7. Dashboard reporting can be supported without duplicating business logic.
