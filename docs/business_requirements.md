# Business Requirements

## Purpose

This document defines the business, reporting, control and decision-support requirements for the Asset-Finance Operations Intelligence System.

The system is intended to consolidate fragmented operational, financial, rider and asset data into a reliable reporting environment for management and operational teams.

## Stakeholders

The main stakeholders are:

* Senior management
* Finance and reconciliation team
* Operations team
* Fleet and maintenance team
* Collections team
* Business intelligence analyst

## Senior Management Requirements

Senior management requires a consolidated view of:

* Expected versus actual collections
* Total outstanding rider balances
* Collection-rate trends
* Active, idle and under-maintenance assets
* Fleet utilization
* High-risk rider accounts
* Reconciliation exceptions
* Major operational issues requiring action

The dashboard should allow management to identify what happened, why it happened and what requires immediate attention.

## Finance and Reconciliation Requirements

The finance and reconciliation team requires the system to:

* Calculate expected weekly repayments
* Compare expected and actual collections
* Calculate rider deductions and net payouts
* Track carried-forward balances
* Identify unmatched transactions
* Detect duplicate payments
* Detect missing or incorrect deductions
* Calculate reconciliation variances
* Produce an exception list for manual review
* Preserve traceable calculation logic

## Operations Requirements

The operations team requires visibility into:

* Active and inactive riders
* Rider earnings performance
* Missed repayments
* Rising outstanding balances
* Prolonged inactivity
* Rider-to-asset assignments
* Accounts requiring follow-up
* Recommended intervention categories

## Fleet and Maintenance Requirements

The fleet and maintenance team requires the system to:

* Track active, idle, under-maintenance, repossessed and completed assets
* Monitor asset-assignment history
* Calculate asset utilization
* Measure maintenance frequency
* Track maintenance downtime
* Identify repeated maintenance incidents
* Compare maintenance cost by asset
* Highlight assets requiring operational attention

## Collections Requirements

The collections team requires the system to:

* Identify overdue rider accounts
* Rank accounts by outstanding balance
* Track consecutive missed repayments
* Flag increasing debt
* Show the reason for each risk classification
* Prioritize collection activities
* Track intervention status

## Functional Requirements

The system must be able to:

1. Import synthetic source data from structured files.
2. Standardize rider, asset, contract and transaction identifiers.
3. Validate required fields.
4. Detect duplicate records.
5. Identify invalid or unmatched records.
6. Store cleaned data in PostgreSQL.
7. Calculate weekly repayment obligations.
8. Calculate actual collections.
9. Calculate rider deductions.
10. Calculate rider net payouts.
11. Calculate outstanding and carried-forward balances.
12. Calculate fleet and maintenance KPIs.
13. Assign rule-based rider-risk classifications.
14. Generate reconciliation exceptions.
15. Create reporting views for Power BI.
16. Present management KPIs and trends.
17. Support drill-down to rider and asset level.
18. Document all major KPI and business rules.

## Data-Quality Requirements

The system should detect and report:

* Missing rider IDs
* Missing asset IDs
* Duplicate transactions
* Duplicate payment references
* Invalid dates
* Negative values where not permitted
* Invalid rider-to-asset assignments
* Payments linked to unknown riders
* Maintenance records linked to unknown assets
* Multiple active assignments for the same asset
* Inconsistent rider and asset statuses

Data-quality issues should be categorized as:

* Corrected automatically
* Rejected
* Flagged for manual review

## Reporting Requirements

### Executive Overview

The dashboard should show:

* Active riders
* Active financed assets
* Expected collections
* Actual collections
* Collection rate
* Total outstanding balance
* Fleet utilization
* Assets under maintenance
* High-risk rider accounts
* Reconciliation exception count

### Collections and Reconciliation

The dashboard should show:

* Expected versus actual collections
* Weekly collection trends
* Rider-level outstanding balances
* Payout calculations
* Reconciliation differences
* Unmatched transactions
* Duplicate or missing deductions
* Accounts requiring manual review

### Fleet and Maintenance

The dashboard should show:

* Asset-status distribution
* Asset utilization
* Idle days
* Maintenance frequency
* Maintenance cost
* Downtime
* Repeated maintenance incidents
* Assets requiring intervention

### Risk and Intervention

The dashboard should show:

* Rider risk level
* Risk score
* Risk reasons
* Missed repayment count
* Earnings trend
* Outstanding-balance trend
* Recommended intervention
* Intervention status

## Non-Functional Requirements

The solution should be:

* Understandable to technical and non-technical users
* Traceable from source data to dashboard result
* Reproducible using documented scripts
* Built using anonymized or synthetic data
* Structured for future expansion
* Easy to review through GitHub
* Free from confidential company information
* Clearly documented

## Assumptions

The project assumes that:

* Each rider has a unique rider identifier.
* Each asset has a unique asset identifier.
* Each contract links one rider to one financed asset.
* Weekly repayment obligations are defined in the contract.
* Rider earnings can be linked to a reporting week.
* Payments and deductions can be traced to a rider.
* Asset-status changes can be recorded over time.
* Maintenance incidents can be linked to an asset.
* Risk classification will initially use documented business rules.

## Acceptance Criteria

The solution will meet the business requirements when it can:

* Produce consistent weekly rider statements
* Calculate expected and actual collections
* Reconcile calculated and recorded payouts
* Detect data-quality and transaction exceptions
* Calculate rider, financial, fleet and maintenance KPIs
* Identify high-risk rider accounts
* Support management action through clear dashboards
* Trace reported figures back to documented calculations
