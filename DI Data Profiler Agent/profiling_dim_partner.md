# Profiling Report: ontology.dim_partner

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | dim_partner |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Partner dimension |
| Row Count | 0 |
| Column Count | 6 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| partner_key | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| partner_id | character varying | NO | 0 | 0 | 0.00% | 0 | 0 |
| partner_name | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| partner_type | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| partner_tier | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| route_to_market | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | partner_key |
| character varying | partner_id, partner_name, partner_type, partner_tier, route_to_market |

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
| partner_key | 0 | No data available |
| partner_id | 0 | No data available |
| partner_name | 0 | No data available |
| partner_type | 0 | No data available |
| partner_tier | 0 | No data available |
| route_to_market | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| partner_key | 0 | No duplicate analysis possible on empty table |
| partner_id | 0 | No duplicate analysis possible on empty table |
| partner_name | 0 | No duplicate analysis possible on empty table |
| partner_type | 0 | No duplicate analysis possible on empty table |
| partner_tier | 0 | No duplicate analysis possible on empty table |
| route_to_market | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| partner_key | N/A | N/A | N/A |

## Date Statistics

No date columns found in this table.

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| partner_id | No rows available for string length statistics or value distribution |
| partner_name | No rows available for string length statistics or value distribution |
| partner_type | No rows available for string length statistics or value distribution |
| partner_tier | No rows available for string length statistics or value distribution |
| route_to_market | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| partner_key | No records present |
| partner_id | No records present |
| partner_name | No records present |
| partner_type | No records present |
| partner_tier | No records present |
| route_to_market | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `partner_key` |
| Mandatory identifier present by design | Pass | `partner_id` is structurally NOT NULL |
| Row availability | Warning | No records available for profiling |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute partner distributions on empty table |
| Text quality checks | Limited | No observed text values |

## Overall Profiling Summary

`ontology.dim_partner` contains the expected partner dimension structure for channel and route-to-market analysis in the Cisco bookings domain, but currently has no rows. This prevents empirical data quality evaluation such as partner-type distribution, route-to-market mix, duplicate partner IDs, or text consistency checks. Structural metadata indicates the table is ready for such profiling once populated.
