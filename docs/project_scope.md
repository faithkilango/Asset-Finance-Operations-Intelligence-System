# Project Scope

## Project Title

Asset-Finance Operations Intelligence System

## Purpose

The purpose of this project is to demonstrate how fragmented financial, operational and asset data can be transformed into a reliable business intelligence system for management reporting and decision-making.

The solution will simulate the operating environment of a rent-to-own mobility business that assigns financed assets to riders and collects repayments from their weekly earnings.

## In Scope

The first version of the project will cover:

* Rider onboarding records
* Asset records
* Rent-to-own contracts
* Rider-to-asset assignments
* Weekly rider earnings
* Repayment obligations
* Actual repayments collected
* Maintenance deductions
* Operational charges
* Rider payout calculations
* Outstanding and carried-forward balances
* Asset-status monitoring
* Maintenance and downtime analysis
* Rule-based rider-risk classification
* Reconciliation exception detection
* Management dashboards

## Out of Scope

The first version will not include:

* Real rider or company records
* Personally identifiable information
* Live GPS integrations
* Live payment-platform integrations
* Production system deployment
* Automated repossession decisions
* Advanced machine-learning deployment
* Mobile or web application development

  These capabilities may be considered as future enhancements
  
## Primary Users

* Senior management
* Operations manager
* Finance and reconciliation team
* Fleet manager
* Collections team
* Business intelligence analyst

## Main Deliverables

1. Synthetic portfolio dataset
2. Relational PostgreSQL database
3. Python cleaning and validation pipeline
4. SQL business logic and reporting views
5. Power BI management dashboard
6. KPI dictionary
7. Data-quality and reconciliation report
8. Findings and recommendations
9. Technical and business documentation

## Dashboard Scope

The Power BI dashboard will contain four main reporting areas:

###### 1. Executive Overview

A summary of collections, outstanding balances, active riders, asset utilization, maintenance status and high-risk accounts.

###### 2. Collections and Reconciliation

Analysis of expected repayments, actual collections, collection rates, payout calculations, outstanding balances and reconciliation exceptions.

###### 3. Fleet and Maintenance

Analysis of active, idle and under-maintenance assets, asset utilization, downtime, maintenance frequency and maintenance costs.

###### 4. Risk and Intervention

Identification of riders with missed repayments, declining earnings, increasing balances, prolonged inactivity or repeated maintenance incidents.

## Project Constraints

The project will use synthetic data rather than confidential company records.

The synthetic data will be designed to reflect realistic operational patterns, including missing values, duplicates, inconsistent identifiers, late repayments, maintenance incidents and reconciliation differences.

The findings will demonstrate analytical methods and business reasoning but will not represent the performance of an actual company.

## Success Criteria

The project will be considered successful when it can:

* Produce consistent weekly rider balances
* Calculate expected and actual collections
* Calculate rider payouts and carried-forward debt
* Detect duplicate, missing and unmatched records
* Identify reconciliation differences
* Measure asset utilization and downtime
* Classify rider accounts using documented risk rules
* Trace dashboard results back to database calculations
* Present clear findings and recommended management actions
