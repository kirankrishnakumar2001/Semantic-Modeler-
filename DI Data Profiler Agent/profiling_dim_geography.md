# Profiling Report: ontology.dim_geography

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | dim_geography |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Geography dimension |
| Row Count | 0 |
| Column Count | 4 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| geography_key | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| region | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| theater | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| country | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | geography_key |
| character varying | region, theater, country |

## NULL Statistics

| Metric | Value |
| --- | --- |
| Total Rows | 0 |
| Columns With Potential NULLs | 3 |
| Observed NULL Values | 0 |
| NULL Percentage Assessment | Not applicable because the table has no rows |

## Distinct Value Statistics

| Column Name | Distinct Count | Assessment |
| --- | --- | --- |
| geography_key | 0 | No data available |
| region | 0 | No data available |
| theater | 0 | No data available |
| country | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| geography_key | 0 | No duplicate analysis possible on empty table |
| region | 0 | No duplicate analysis possible on empty table |
| theater | 0 | No duplicate analysis possible on empty table |
| country | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| geography_key | N/A | N/A | N/A |

## Date Statistics

No date columns found in this table.

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| region | No rows available for string length statistics or value distribution |
| theater | No rows available for string length statistics or value distribution |
| country | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| geography_key | No records present |
| region | No records present |
| theater | No records present |
| country | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `geography_key` |
| Row availability | Warning | No records available for profiling |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute geographic distributions on empty table |
| Text quality checks | Limited | No observed text values |

## Overall Profiling Summary

`ontology.dim_geography` exists and is structurally simple, with 4 columns intended to describe sales geography at region, theater, and country levels. The table currently contains no data, so the profiling outcome is limited to schema-level inspection only. No value distributions, missing data patterns, or text statistics can be derived until records are loaded.
