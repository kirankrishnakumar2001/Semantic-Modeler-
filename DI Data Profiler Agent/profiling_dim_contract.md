# Profiling Report: ontology.dim_contract

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | dim_contract |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Contract dimension |
| Row Count | 0 |
| Column Count | 5 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| contract_key | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| contract_type | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| term_months | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| auto_renew_flag | character | YES | 0 | 0 | 0.00% | 0 | 0 |
| coverage_level | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | contract_key, term_months |
| character | auto_renew_flag |
| character varying | contract_type, coverage_level |

## NULL Statistics

| Metric | Value |
| --- | --- |
| Total Rows | 0 |
| Columns With Potential NULLs | 4 |
| Observed NULL Values | 0 |
| NULL Percentage Assessment | Not applicable because the table has no rows |

## Distinct Value Statistics

| Column Name | Distinct Count | Assessment |
| --- | --- | --- |
| contract_key | 0 | No data available |
| contract_type | 0 | No data available |
| term_months | 0 | No data available |
| auto_renew_flag | 0 | No data available |
| coverage_level | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| contract_key | 0 | No duplicate analysis possible on empty table |
| contract_type | 0 | No duplicate analysis possible on empty table |
| term_months | 0 | No duplicate analysis possible on empty table |
| auto_renew_flag | 0 | No duplicate analysis possible on empty table |
| coverage_level | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| contract_key | N/A | N/A | N/A |
| term_months | N/A | N/A | N/A |

## Date Statistics

No date columns found in this table.

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| contract_type | No rows available for string length statistics or value distribution |
| auto_renew_flag | No rows available for string length statistics or value distribution |
| coverage_level | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| contract_key | No records present |
| contract_type | No records present |
| term_months | No records present |
| auto_renew_flag | No records present |
| coverage_level | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `contract_key` |
| Row availability | Warning | No records available for profiling |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute distributions on empty table |
| Numeric range checks | Limited | No observed data values |
| Text quality checks | Limited | No observed text values |

## Overall Profiling Summary

`ontology.dim_contract` is structurally valid and available in PostgreSQL database `ontology`, but it currently contains no rows. As a result, profiling is limited to metadata-based assessment only. The table has 5 columns, including integer and text attributes aligned with the contract dimension in the Cisco bookings star schema. To complete a full data quality and distribution analysis, the table must be populated with business records.
