## 🚀 Key Impact

- Identified **$16.7M+ in financial discrepancies**
- Reduced reconciliation time from **hours to minutes**
- Automated detection of missing and inconsistent transactions

# Bank Reconciliation & Exception Report System  
**Excel · Power Query (M) · ETL Architecture**

---

## Overview

This project automates the reconciliation of financial records between an **internal ledger** and an **external bank statement**, helping finance teams identify discrepancies, missing transactions, and operational risks quickly and accurately.

Built in **Excel + Power Query**, the solution handles high-volume data, standardizes inconsistent transaction formats, and produces a fully traceable exception report for audit and review.

---

## Business Context

FinFlow Solutions, a mid-sized fintech company, was processing over **1,000 monthly transactions** across two systems: an internal ledger and an external bank statement.

As operations scaled, the finance team began noticing inconsistencies between both sources, but the reconciliation process was:

- Fully manual
- Time-consuming
- Dependent on one person’s institutional knowledge
- Lacking audit visibility and exception classification

The company needed a structured and scalable way to identify:
- Which transactions matched
- Which were missing on either side
- Which had amount discrepancies
- Which represented critical status conflicts

---

## The Problem

Manual reconciliation in high-volume financial environments often fails because of:

- **Data Friction:** Transaction IDs entered inconsistently across systems  
  (`TXN-001`, `txn_001`, `TXN001`)
- **Format Conflicts:** Amounts stored as strings instead of numeric values  
  (`$2,500.00 USD` vs `2500`)
- **Audit Gaps:** No systematic way to identify records missing on one side
- **Status Mismatches:** Records approved internally but voided externally

---

## The Solution

This project implements a **3-layer ETL reconciliation architecture** in Excel and Power Query that:

- Cleans and standardizes transaction identifiers
- Converts mixed currency formats into numeric values
- Reconciles records across both sources
- Classifies each transaction into audit-ready categories
- Generates a clear exception report for immediate action

No manual matching. No hidden logic. Every discrepancy is documented and traceable.

---

## Results

| Audit Result | Transactions | Discrepancy |
|---|---:|---:|
| Match | 851 | $0 |
| Amount Mismatch | 90 | -$3,763,696 |
| Missing in Internal Ledger | 38 | $20,468,134 |
| CRITICAL: Status Conflict | 19 | Operational Risk |
| **TOTAL** | **998** | **$16,704,438 identified** |

### Business Impact
- Reduced reconciliation time from **hours to minutes**
- Identified **$16.7M+ in discrepancies**
- Delivered full visibility over financial inconsistencies
- Improved traceability and exception management

---

## Technical Architecture

The solution follows a **3-layer ETL design** to improve maintainability, clarity, and scalability.

### 1. Staging Layer
Raw source ingestion from:
- Internal Ledger
- External Bank Statement

### 2. Transformation Layer
Data preparation and standardization, including:

#### Transaction ID Normalization
A custom Power Query function (`fnNormalizeID`) standardizes alphanumeric identifiers using logic such as:

- `Text.Upper`
- `Text.Trim`
- `Text.Select`

Example:

- `" txn_001 "` → `"TXN001"`

#### Currency & Numeric Parsing
Complex currency strings are converted into fixed decimal values for reliable comparison.

Example:

- `"$2,500.00 USD"` → `2500.00`

### 3. Load / Reporting Layer
The transformed data is loaded into reconciliation and reporting outputs for audit review.

---

## Reconciliation Logic

The project uses Power Query joins and exception rules to classify records into meaningful audit categories.

### Matching Logic
- **Full Outer Join** to create a master reconciliation view
- **Anti-Joins** to isolate unmatched records on either side

### Exception Categories
- **Match** — Transaction exists in both sources with no discrepancy
- **Amount Mismatch** — Transaction exists in both, but values differ
- **Missing in Internal Ledger** — Present externally, absent internally
- **Missing in External Statement** — Present internally, absent externally
- **Status Conflict** — Internal status differs critically from external status  
  Example: `Approved` vs `Voided`

---

## File Structure

| Sheet | Description |
|---|---|
| `Executive_Summary_KPIs` | High-level audit metrics and reconciliation summary |
| `Reconciliation_Master` | Full cross-validated transaction table |
| `Financial_Exceptions_Report` | Filtered view of exception records requiring action |
| `Internal_Ledger_1k` | Raw internal source data |
| `External_Statement_1k` | Raw external source data |

---

## Tech Stack

- **Excel** — Reporting layer and user-facing structure
- **Power Query (M)** — ETL logic, normalization, joins, and data transformation
- **DAX** — KPI calculations and audit flag logic

---

## Key Design Principles

- **Full traceability** from raw source to final exception report
- **No hidden transformations**
- **Actionable outputs** for finance and audit teams
- **Reusable structure** for similar reconciliation workflows
- **Maintainable logic** through modular query design
- **Parameter tables** for easier updates by non-technical users

---

## Use Cases

This solution can be adapted for:

- Bank vs. ledger reconciliation
- ERP vs. payment processor validation
- Internal finance audits
- Exception reporting workflows
- Transaction integrity checks in fintech or accounting environments

---

## What This Project Demonstrates

This project showcases my ability to:

- Build practical ETL solutions in Excel and Power Query
- Solve high-volume reconciliation problems
- Design audit-friendly reporting systems
- Translate messy financial data into structured, decision-ready outputs
- Combine technical implementation with business impact

---

## Author

**Diana Novoa**  
Financial Data Automation | Excel | Power Query | SQL | Reconciliation Systems

---

## Notes

This solution reflects a real-world approach to financial reconciliation, focusing on scalability, traceability, and actionable exception reporting for finance teams.

