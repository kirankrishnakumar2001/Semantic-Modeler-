# Profiling Report: ontology.dim_customer

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | dim_customer |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Customer dimension |
| Row Count | 0 |
| Column Count | 8 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| customer_key | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| customer_id | character varying | NO | 0 | 0 | 0.00% | 0 | 0 |
| customer_name | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| segment | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| industry | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| account_tier | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| hq_country | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| hq_region | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | customer_key |
| character varying | customer_id, customer_name, segment, industry, account_tier, hq_country, hq_region |

## NULL Statistics

| Metric | Value |
| --- | --- |
| Total Rows | 0 |
| Columns With Potential NULLs | 6 |
| Observed NULL Values | 0 |
| NULL Percentage Assessment | Not applicable because the table has no rows |

## Distinct Value Statistics

| Column Name | Distinct Count | Assessment |
| --- | --- | --- |
| customer_key | 0 | No data available |
| customer_id | 0 | No data available |
| customer_name | 0 | No data available |
| segment | 0 | No data available |
| industry | 0 | No data available |
| account_tier | 0 | No data available |
| hq_country | 0 | No data available |
| hq_region | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| customer_key | 0 | No duplicate analysis possible on empty table |
| customer_id | 0 | No duplicate analysis possible on empty table |
| customer_name | 0 | No duplicate analysis possible on empty table |
| segment | 0 | No duplicate analysis possible on empty table |
| industry | 0 | No duplicate analysis possible on empty table |
| account_tier | 0 | No duplicate analysis possible on empty table |
| hq_country | 0 | No duplicate analysis possible on empty table |
| hq_region | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| customer_key | N/A | N/A | N/A |

## Date Statistics

No date columns found in this table.

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| customer_id | No rows available for string length statistics or value distribution |
| customer_name | No rows available for string length statistics or value distribution |
| segment | No rows available for string length statistics or value distribution |
| industry | No rows available for string length statistics or value distribution |
| account_tier | No rows available for string length statistics or value distribution |
| hq_country | No rows available for string length statistics or value distribution |
| hq_region | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| customer_key | No records present |
| customer_id | No records present |
| customer_name | No records present |
| segment | No records present |
| industry | No records present |
| account_tier | No records present |
| hq_country | No records present |
| hq_region | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `customer_key` |
| Mandatory identifier present by design | Pass | `customer_id` is structurally NOT NULL |
| Row availability | Warning | No records available for profiling |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute distributions on empty table |
| Text quality checks | Limited | No observed text values |

## Overall Profiling Summary

`ontology.dim_customer` is present and structurally well-defined with 8 columns, including one integer surrogate key and seven business descriptor fields. However, the table currently contains no rows, so no empirical profiling results such as distributions, text length patterns, duplicates, or missing-data rates can be produced from actual data. Only metadata-driven quality observations are currently possible.
