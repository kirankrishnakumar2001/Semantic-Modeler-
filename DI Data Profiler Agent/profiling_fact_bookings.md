# Profiling Report: ontology.fact_bookings

## Table Information

| Attribute | Value |
| --- | --- |
| Database Name | ontology |
| Schema Name | ontology |
| Table Name | fact_bookings |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Table Role | Booking transaction fact table |
| Grain | One booking transaction / order-line booking event |
| Row Count | 0 |
| Column Count | 18 |
| Profiling Status | Table exists but contains no rows |

## Column Profile Summary

| Column Name | Data Type | Nullable | Non-Null Count | Null Count | Null % | Distinct Count | Duplicate Count* |
| --- | --- | --- | --- | --- | --- | --- | --- |
| booking_id | integer | NO | 0 | 0 | 0.00% | 0 | 0 |
| order_number | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| order_line_number | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| date_key | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| customer_key | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| product_key | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| partner_key | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| geography_key | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| sales_rep_key | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| contract_key | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| booking_type | character varying | YES | 0 | 0 | 0.00% | 0 | 0 |
| is_renewal | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| quantity | integer | YES | 0 | 0 | 0.00% | 0 | 0 |
| unit_list_price_usd | numeric | YES | 0 | 0 | 0.00% | 0 | 0 |
| discount_pct | numeric | YES | 0 | 0 | 0.00% | 0 | 0 |
| booking_amount_usd | numeric | YES | 0 | 0 | 0.00% | 0 | 0 |
| acv_usd | numeric | YES | 0 | 0 | 0.00% | 0 | 0 |
| tcv_usd | numeric | YES | 0 | 0 | 0.00% | 0 | 0 |

\* Duplicate Count interpreted as `non_null_count - distinct_count`. For empty tables this is 0 for all columns.

## Column Data Types

| Data Type | Column(s) |
| --- | --- |
| integer | booking_id, order_line_number, date_key, customer_key, product_key, partner_key, geography_key, sales_rep_key, contract_key, is_renewal, quantity |
| character varying | order_number, booking_type |
| numeric | unit_list_price_usd, discount_pct, booking_amount_usd, acv_usd, tcv_usd |

## NULL Statistics

| Metric | Value |
| --- | --- |
| Total Rows | 0 |
| Columns With Potential NULLs | 17 |
| Observed NULL Values | 0 |
| NULL Percentage Assessment | Not applicable because the table has no rows |

## Distinct Value Statistics

| Column Name | Distinct Count | Assessment |
| --- | --- | --- |
| booking_id | 0 | No data available |
| order_number | 0 | No data available |
| order_line_number | 0 | No data available |
| date_key | 0 | No data available |
| customer_key | 0 | No data available |
| product_key | 0 | No data available |
| partner_key | 0 | No data available |
| geography_key | 0 | No data available |
| sales_rep_key | 0 | No data available |
| contract_key | 0 | No data available |
| booking_type | 0 | No data available |
| is_renewal | 0 | No data available |
| quantity | 0 | No data available |
| unit_list_price_usd | 0 | No data available |
| discount_pct | 0 | No data available |
| booking_amount_usd | 0 | No data available |
| acv_usd | 0 | No data available |
| tcv_usd | 0 | No data available |

## Duplicate Statistics

| Column Name | Duplicate Count | Assessment |
| --- | --- | --- |
| booking_id | 0 | No duplicate analysis possible on empty table |
| order_number | 0 | No duplicate analysis possible on empty table |
| order_line_number | 0 | No duplicate analysis possible on empty table |
| date_key | 0 | No duplicate analysis possible on empty table |
| customer_key | 0 | No duplicate analysis possible on empty table |
| product_key | 0 | No duplicate analysis possible on empty table |
| partner_key | 0 | No duplicate analysis possible on empty table |
| geography_key | 0 | No duplicate analysis possible on empty table |
| sales_rep_key | 0 | No duplicate analysis possible on empty table |
| contract_key | 0 | No duplicate analysis possible on empty table |
| booking_type | 0 | No duplicate analysis possible on empty table |
| is_renewal | 0 | No duplicate analysis possible on empty table |
| quantity | 0 | No duplicate analysis possible on empty table |
| unit_list_price_usd | 0 | No duplicate analysis possible on empty table |
| discount_pct | 0 | No duplicate analysis possible on empty table |
| booking_amount_usd | 0 | No duplicate analysis possible on empty table |
| acv_usd | 0 | No duplicate analysis possible on empty table |
| tcv_usd | 0 | No duplicate analysis possible on empty table |

## Numeric Statistics

| Column Name | Min | Max | Avg |
| --- | --- | --- | --- |
| booking_id | N/A | N/A | N/A |
| order_line_number | N/A | N/A | N/A |
| date_key | N/A | N/A | N/A |
| customer_key | N/A | N/A | N/A |
| product_key | N/A | N/A | N/A |
| partner_key | N/A | N/A | N/A |
| geography_key | N/A | N/A | N/A |
| sales_rep_key | N/A | N/A | N/A |
| contract_key | N/A | N/A | N/A |
| is_renewal | N/A | N/A | N/A |
| quantity | N/A | N/A | N/A |
| unit_list_price_usd | N/A | N/A | N/A |
| discount_pct | N/A | N/A | N/A |
| booking_amount_usd | N/A | N/A | N/A |
| acv_usd | N/A | N/A | N/A |
| tcv_usd | N/A | N/A | N/A |

## Date Statistics

No date-typed columns exist in this fact table. Time analysis is expected through the `date_key` foreign key to `dim_date`.

## Text Statistics

| Column Name | Text Profiling Status |
| --- | --- |
| order_number | No rows available for string length statistics or value distribution |
| booking_type | No rows available for string length statistics or value distribution |

## Value Distribution Summary

No value distribution could be generated because the table contains 0 rows.

## Missing Data Statistics

| Column Name | Missing Data Observation |
| --- | --- |
| booking_id | No records present |
| order_number | No records present |
| order_line_number | No records present |
| date_key | No records present |
| customer_key | No records present |
| product_key | No records present |
| partner_key | No records present |
| geography_key | No records present |
| sales_rep_key | No records present |
| contract_key | No records present |
| booking_type | No records present |
| is_renewal | No records present |
| quantity | No records present |
| unit_list_price_usd | No records present |
| discount_pct | No records present |
| booking_amount_usd | No records present |
| acv_usd | No records present |
| tcv_usd | No records present |

## Data Quality Summary

| Quality Indicator | Status | Details |
| --- | --- | --- |
| Table existence | Pass | Table verified in schema ontology |
| Primary key defined | Pass | `booking_id` |
| Referential structure | Pass | Foreign keys defined to date, customer, product, partner, geography, sales rep, and contract dimensions |
| Row availability | Warning | No booking transactions available for profiling |
| Completeness assessment | Limited | Cannot assess completeness beyond structural nullability because table is empty |
| Distribution assessment | Limited | Cannot compute booking mix, price, discount, or revenue distributions |
| Numeric quality checks | Limited | No observed numeric values for range or outlier inspection |
| Business metric quality | Limited | Cannot evaluate ACV, TCV, booking amount, renewal mix, or quantity behavior |

## Overall Profiling Summary

`ontology.fact_bookings` is the central fact table in the Cisco Sales Bookings and Revenue Analytics star schema and is structurally modeled at booking transaction / order-line grain. It contains 18 columns, including foreign keys to seven conformed dimensions and the core commercial measures required for bookings analytics. However, the table currently contains no rows, so all data-driven profiling outputs such as measure distributions, duplicate patterns, completeness metrics, and numeric ranges are unavailable. Profiling confirms that the fact table structure is present and ready for business use once data is loaded.
