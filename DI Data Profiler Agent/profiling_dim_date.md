# Profiling Report: ontology.dim_date

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | dim_date |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Date dimension |
| Row Count | 0 |
| Column Count | 7 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| date_key | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| full_date | date | NO | 0 | 0 | 0.00% | 0 | 0 |
| month_name | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| calendar_year | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| fiscal_year | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| fiscal_quarter | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| fiscal_period_seq | integer | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | date_key, calendar_year, fiscal_period_seq |
| date | full_date |
| character varying | month_name, fiscal_year, fiscal_quarter |

## NULL Statistics

| Metric | Value |
| --- | --- |
| Total Rows | 0 |
| Columns With Potential NULLs | 5 |
| Observed NULL Values | 0 |
| NULL Percentage Assessment | Not applicable because the table has no rows |

## Distinct Value Statistics

| Column Name | Distinct Count | Assessment |
| --- | --- | --- |
| date_key | 0 | No data available |
| full_date | 0 | No data available |
| month_name | 0 | No data available |
| calendar_year | 0 | No data available |
| fiscal_year | 0 | No data available |
| fiscal_quarter | 0 | No data available |
| fiscal_period_seq | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| date_key | 0 | No duplicate analysis possible on empty table |
| full_date | 0 | No duplicate analysis possible on empty table |
| month_name | 0 | No duplicate analysis possible on empty table |
| calendar_year | 0 | No duplicate analysis possible on empty table |
| fiscal_year | 0 | No duplicate analysis possible on empty table |
| fiscal_quarter | 0 | No duplicate analysis possible on empty table |
| fiscal_period_seq | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| date_key | N/A | N/A | N/A |
| calendar_year | N/A | N/A | N/A |
| fiscal_period_seq | N/A | N/A | N/A |

## Date Statistics

| Column Name | Min Date | Max Date |
| --- | --- | --- |
| full_date | N/A | N/A |

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| month_name | No rows available for string length statistics or value distribution |
| fiscal_year | No rows available for string length statistics or value distribution |
| fiscal_quarter | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| date_key | No records present |
| full_date | No records present |
| month_name | No records present |
| calendar_year | No records present |
| fiscal_year | No records present |
| fiscal_quarter | No records present |
| fiscal_period_seq | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `date_key` |
| Mandatory date column defined | Pass | `full_date` is structurally NOT NULL |
| Row availability | Warning | No records available for profiling |
| Date range assessment | Limited | No observed dates available |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute distributions on empty table |

## Overall Profiling Summary

`ontology.dim_date` is structurally ready for time-based analysis, with 7 columns covering standard date and fiscal attributes. The schema suggests it is intended to support calendar and fiscal reporting in the Cisco bookings star schema. However, because the table currently contains 0 records, no actual date range, fiscal distribution, or completeness profile can be derived from the data.
