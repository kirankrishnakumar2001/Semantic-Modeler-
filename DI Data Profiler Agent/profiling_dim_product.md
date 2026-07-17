# Profiling Report: ontology.dim_product

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | dim_product |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Product dimension |
| Row Count | 0 |
| Column Count | 7 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| product_key | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| product_id | character varying | NO | 0 | 0 | 0.00% | 0 | 0 |
| product_name | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| product_family | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| technology_domain | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| offer_type | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| business_entity | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | product_key |
| character varying | product_id, product_name, product_family, technology_domain, offer_type, business_entity |

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
| product_key | 0 | No data available |
| product_id | 0 | No data available |
| product_name | 0 | No data available |
| product_family | 0 | No data available |
| technology_domain | 0 | No data available |
| offer_type | 0 | No data available |
| business_entity | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| product_key | 0 | No duplicate analysis possible on empty table |
| product_id | 0 | No duplicate analysis possible on empty table |
| product_name | 0 | No duplicate analysis possible on empty table |
| product_family | 0 | No duplicate analysis possible on empty table |
| technology_domain | 0 | No duplicate analysis possible on empty table |
| offer_type | 0 | No duplicate analysis possible on empty table |
| business_entity | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| product_key | N/A | N/A | N/A |

## Date Statistics

No date columns found in this table.

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| product_id | No rows available for string length statistics or value distribution |
| product_name | No rows available for string length statistics or value distribution |
| product_family | No rows available for string length statistics or value distribution |
| technology_domain | No rows available for string length statistics or value distribution |
| offer_type | No rows available for string length statistics or value distribution |
| business_entity | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| product_key | No records present |
| product_id | No records present |
| product_name | No records present |
| product_family | No records present |
| technology_domain | No records present |
| offer_type | No records present |
| business_entity | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `product_key` |
| Mandatory identifier present by design | Pass | `product_id` is structurally NOT NULL |
| Row availability | Warning | No records available for profiling |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute product mix or domain distributions on empty table |
| Text quality checks | Limited | No observed text values |

## Overall Profiling Summary

`ontology.dim_product` is a 7-column product dimension intended to support analysis across product family, technology domain, offer type, and business entity. The table exists and is structurally valid, but no data is currently stored in it. Because of that, only metadata-level profiling could be completed and all observed data statistics remain unavailable.
