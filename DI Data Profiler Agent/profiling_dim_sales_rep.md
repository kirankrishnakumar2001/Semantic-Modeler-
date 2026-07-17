# Profiling Report: ontology.dim_sales_rep

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | dim_sales_rep |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Sales representative dimension |
| Row Count | 0 |
| Column Count | 6 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| sales_rep_key | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| rep_id | character varying | NO | 0 | 0 | 0.00% | 0 | 0 |
| rep_name | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| sales_role | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| sales_team | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| segment_covered | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | sales_rep_key |
| character varying | rep_id, rep_name, sales_role, sales_team, segment_covered |

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
| sales_rep_key | 0 | No data available |
| rep_id | 0 | No data available |
| rep_name | 0 | No data available |
| sales_role | 0 | No data available |
| sales_team | 0 | No data available |
| segment_covered | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| sales_rep_key | 0 | No duplicate analysis possible on empty table |
| rep_id | 0 | No duplicate analysis possible on empty table |
| rep_name | 0 | No duplicate analysis possible on empty table |
| sales_role | 0 | No duplicate analysis possible on empty table |
| sales_team | 0 | No duplicate analysis possible on empty table |
| segment_covered | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| sales_rep_key | N/A | N/A | N/A |

## Date Statistics

No date columns found in this table.

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| rep_id | No rows available for string length statistics or value distribution |
| rep_name | No rows available for string length statistics or value distribution |
| sales_role | No rows available for string length statistics or value distribution |
| sales_team | No rows available for string length statistics or value distribution |
| segment_covered | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| sales_rep_key | No records present |
| rep_id | No records present |
| rep_name | No records present |
| sales_role | No records present |
| sales_team | No records present |
| segment_covered | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `sales_rep_key` |
| Mandatory identifier present by design | Pass | `rep_id` is structurally NOT NULL |
| Row availability | Warning | No records available for profiling |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute sales team or role distributions on empty table |
| Text quality checks | Limited | No observed text values |

## Overall Profiling Summary

`ontology.dim_sales_rep` is available in the ontology schema and contains the expected structure for sales representative analysis, including role, team, and segment coverage fields. Since the table currently has no rows, the profiling report is restricted to schema and metadata characteristics only. Data-driven quality checks will become possible after loading representative records.
