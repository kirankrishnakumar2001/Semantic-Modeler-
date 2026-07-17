# Semantic Summary

## Semantic Overview

| Section | Value |
| --- | --- |
| Business Subject Area | Cisco Sales Bookings and Revenue Analytics |
| Data Domain Description | Star-schema analytical model for Cisco booking transactions at order-line grain with conformed dimensions for customer, product, partner, geography, sales representative, contract, and date. |
| Business Value Proposition | Provides a governed semantic foundation for consistent analysis of bookings, ACV, TCV, quantity, discounting, partner contribution, product mix, renewals, and fiscal performance across Cisco sales operations. |
| Business Capabilities Enabled | Booking performance reporting; customer and segment analysis; product portfolio analysis; partner and route-to-market analysis; geography reporting; sales performance management; contract and renewal analysis; fiscal period reporting; executive dashboards; semantic reuse for downstream analytics and knowledge modeling |
| Business Question 1 | What is total booking amount by fiscal year, fiscal quarter, region, and product family? |
| Business Question 2 | How do renewal bookings and ACV/TCV vary by contract type, offer type, and customer segment? |
| Business Question 3 | What is partner contribution to bookings by route to market, theater, and sales team? |

## Input Validation

| Validation Check | Status | Details |
| --- | --- | --- |
| Data Dictionary readability | Pass | PostgreSQL data dictionary for database `ontology` was provided in readable markdown form. |
| Business Glossary availability | Pass | Business glossary–enriched data dictionary was provided and readable. |
| Business Process / Metrics / Relationships document readability | Pass | `Cisco_Bookings_Data_Model_and_Process.docx` was read successfully. |
| Business Domain Context readability | Pass | `Business Domain Context.txt` was read successfully. |
| Missing tables | Pass | No missing business tables identified from supplied schema scope. |
| Duplicate tables | Pass | 8 unique tables identified. |
| Duplicate glossary terms | Pass | No duplicate glossary terms explicitly identified in supplied glossary. |
| Invalid column definitions | Pass | Column definitions are structurally valid and typed. |
| Missing primary keys | Pass | All 8 tables have primary keys. |
| Broken foreign keys | Pass | All 7 declared foreign keys resolve to existing parent primary keys. |
| Invalid glossary mappings | Partial Pass | Most mappings are direct; some business definitions are inferred because all tables are empty and source comments are unavailable. |
| Data availability for semantic validation | Warning | All 8 tables have row count = 0, so empirical validation of values, domains, and measure behavior is not possible. |
| Table/column descriptions in source catalog | Warning | Table comments and column comments were not available in source metadata. |

## Schema Discovery Summary

| Schema Element | Count | Details |
| --- | --- | --- |
| Total Tables | 8 | `fact_bookings` plus 7 dimensions |
| Fact Tables | 1 | `fact_bookings` |
| Dimension Tables | 7 | `dim_contract`, `dim_customer`, `dim_date`, `dim_geography`, `dim_partner`, `dim_product`, `dim_sales_rep` |
| Lookup Tables | 0 | None explicitly modeled |
| Bridge Tables | 0 | None identified |
| Total Columns | 61 | Across all 8 tables |
| Primary Keys | 8 | One per table |
| Foreign Keys | 7 | All from `fact_bookings` to dimensions |
| Constraints | 15 | 8 PK + 7 FK |

## Semantic Domain Discovery

| Domain Name | Domain Description | Business Purpose | Tables |
| --- | --- | --- | --- |
| Sales Bookings | Central booking transaction domain capturing commercial booking events and core measures at order-line grain. | Measure demand, bookings performance, renewal mix, and contract value. | `fact_bookings` |
| Customer | Customer account master context for segmentation and industry analysis. | Analyze bookings by account, segment, industry, and headquarters geography. | `dim_customer` |
| Product | Product and offer master context across families and technology areas. | Analyze portfolio mix, offer types, and business entity performance. | `dim_product` |
| Partner / Channel | Partner and route-to-market context for indirect sales analysis. | Measure partner contribution and channel effectiveness. | `dim_partner` |
| Geography | Sales geography hierarchy used for regional reporting. | Support analysis by region, theater, and country. | `dim_geography` |
| Sales Organization | Sales ownership and coverage context. | Analyze bookings by sales representative, role, team, and segment coverage. | `dim_sales_rep` |
| Contract | Contract and entitlement context for support and subscription analysis. | Analyze term, coverage, renewal behavior, ACV, and TCV relationships. | `dim_contract` |
| Time | Calendar and fiscal reporting context. | Enable time-based reporting and fiscal rollups. | `dim_date` |

## Glossary Mapping Summary

| Category | Count | Notes |
| --- | --- | --- |
| Total Glossary Terms | 69 | 8 table-level terms + 61 column-level terms |
| Mapped Terms | 69 | Every supplied glossary term maps to a table or column in schema |
| Glossary Coverage Percentage | 100.00% | Based on supplied glossary terms mapped to technical elements |
| Unmapped Columns | 0 | All 61 columns have glossary mappings in supplied enriched dictionary |
| Duplicate Mappings | 0 | No duplicate technical mappings detected |
| Ambiguous Mappings | 4 | `business_entity`, `booking_type`, `is_renewal`, and `auto_renew_flag` have inferred business semantics due to lack of data values |

## Business Entity Discovery

| Business Entity | Technical Table | Entity Type | Business Key(s) | Attributes | Measures | Hierarchies / Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Booking Transaction | `fact_bookings` | Fact | `booking_id`; operational grouping: `order_number`, `order_line_number` | booking_type, is_renewal, all dimension foreign keys | quantity, unit_list_price_usd, discount_pct, booking_amount_usd, acv_usd, tcv_usd | Grain explicitly stated as one booking transaction / order-line booking event |
| Customer | `dim_customer` | Dimension | `customer_id`; surrogate `customer_key` | customer_name, segment, industry, account_tier, hq_country, hq_region | None explicit | Hierarchy inferred: hq_region > hq_country > customer_name |
| Product | `dim_product` | Dimension | `product_id`; surrogate `product_key` | product_name, product_family, technology_domain, offer_type, business_entity | None explicit | Hierarchy inferred: business_entity > technology_domain > product_family > product_name |
| Partner | `dim_partner` | Dimension | `partner_id`; surrogate `partner_key` | partner_name, partner_type, partner_tier, route_to_market | None explicit | Hierarchy inferred: route_to_market > partner_type > partner_tier > partner_name |
| Geography | `dim_geography` | Dimension | surrogate `geography_key` | region, theater, country | None explicit | Explicit hierarchy from naming: region > theater > country |
| Sales Representative | `dim_sales_rep` | Dimension | `rep_id`; surrogate `sales_rep_key` | rep_name, sales_role, sales_team, segment_covered | None explicit | Hierarchy inferred: sales_team > sales_role > rep_name |
| Contract | `dim_contract` | Dimension | surrogate `contract_key` | contract_type, term_months, auto_renew_flag, coverage_level | None explicit | Contract term and coverage analysis support renewal metrics |
| Date | `dim_date` | Dimension | `full_date`; surrogate `date_key` | month_name, calendar_year, fiscal_year, fiscal_quarter, fiscal_period_seq | None explicit | Hierarchy inferred: fiscal_year > fiscal_quarter > full_date; calendar_year > month_name > full_date |

## Relationship Discovery

| Relationship Name | Parent Entity | Child Entity | Relationship Type | Cardinality | Confidence Score | Basis |
| --- | --- | --- | --- | --- | --- | --- |
| Date to Booking Transaction | Date | Booking Transaction | Dimensional foreign key | One-to-Many | 1.00 | Explicit FK `fact_bookings.date_key -> dim_date.date_key` |
| Customer to Booking Transaction | Customer | Booking Transaction | Dimensional foreign key | One-to-Many | 1.00 | Explicit FK `fact_bookings.customer_key -> dim_customer.customer_key` |
| Product to Booking Transaction | Product | Booking Transaction | Dimensional foreign key | One-to-Many | 1.00 | Explicit FK `fact_bookings.product_key -> dim_product.product_key` |
| Partner to Booking Transaction | Partner | Booking Transaction | Dimensional foreign key | One-to-Many | 1.00 | Explicit FK `fact_bookings.partner_key -> dim_partner.partner_key` |
| Geography to Booking Transaction | Geography | Booking Transaction | Dimensional foreign key | One-to-Many | 1.00 | Explicit FK `fact_bookings.geography_key -> dim_geography.geography_key` |
| Sales Representative to Booking Transaction | Sales Representative | Booking Transaction | Dimensional foreign key | One-to-Many | 1.00 | Explicit FK `fact_bookings.sales_rep_key -> dim_sales_rep.sales_rep_key` |
| Contract to Booking Transaction | Contract | Booking Transaction | Dimensional foreign key | One-to-Many | 1.00 | Explicit FK `fact_bookings.contract_key -> dim_contract.contract_key` |
| Customer Headquarters to Geography | Customer | Geography | Semantic contextual association | Many-to-One inferred | 0.55 | Based on `hq_country` and `hq_region` naming only; no explicit FK |
| Product to Contract Applicability | Product | Contract | Semantic business association | Many-toMany conceptual | 0.52 | Inferred from business process that support/subscription offers attach to contracts; not represented by direct FK |

## Semantic Metrics

### Overall Metrics

| Metric | Value |
| --- | --- |
| Total Tables | 8 |
| Total Columns | 61 |
| Total Relationships | 9 |
| Total Domains | 8 |
| Total Measures | 6 |
| Total Glossary Terms | 69 |
| Mapped Terms | 69 |
| Glossary Coverage Percentage | 100.00% |

### Per-Domain Metrics

| Domain Name | Entity Count | Attribute Count | Measure Count | Glossary Coverage Percentage | Domain Status |
| --- | --- | --- | --- | --- | --- |
| Sales Bookings | 1 | 12 | 6 | 100.00% | Structurally complete; data unavailable |
| Customer | 1 | 6 | 0 | 100.00% | Structurally complete; data unavailable |
| Product | 1 | 6 | 0 | 100.00% | Structurally complete; data unavailable |
| Partner / Channel | 1 | 5 | 0 | 100.00% | Structurally complete; data unavailable |
| Geography | 1 | 3 | 0 | 100.00% | Structurally complete; data unavailable |
| Sales Organization | 1 | 5 | 0 | 100.00% | Structurally complete; data unavailable |
| Contract | 1 | 4 | 0 | 100.00% | Structurally complete; data unavailable |
| Time | 1 | 6 | 0 | 100.00% | Structurally complete; data unavailable |

## Semantic Quality & Reasoning

### Design Observations

| Observation Type | Details |
| --- | --- |
| Modeling Style | The schema is a clean Kimball star schema centered on `fact_bookings`. |
| Fact Grain | Grain is explicitly defined as one booking transaction / order-line booking event. |
| Conformance | All dimensions are conformed to the single fact via explicit foreign keys. |
| Analytical Focus | Model is optimized for sales bookings, renewal, channel, product, and fiscal analysis. |
| Simplicity | No bridge tables or snowflaked hierarchies are present, making semantic consumption straightforward. |

### Glossary Health

| Check | Status | Details |
| --- | --- | --- |
| Table glossary coverage | Good | All 8 tables have business glossary entries. |
| Column glossary coverage | Good | All 61 columns have business glossary entries. |
| Definition grounding | Moderate | Definitions are structurally strong but many rely on inference because source metadata comments and row-level data are absent. |
| Acronym treatment | Good | ACV, TCV, FY, FQ, and RTM are explicitly explained. |
| Mapping precision | Moderate | High for explicit keys and measures; moderate for a few coded/derived business terms lacking observed values. |

### Recommendations

| Priority | Recommendation |
| --- | --- |
| High | Populate all tables to enable validation of coded domains such as `booking_type`, `is_renewal`, and `auto_renew_flag`. |
| High | Add source table and column comments to improve semantic precision and reduce inference dependency. |
| Medium | Define explicit data quality rules for measure consistency, e.g., booking amount vs quantity × price × discount, and ACV applicability for subscription offers. |
| Medium | Consider a dedicated renewal date or contract expiration attribute if renewal capture rate is a required KPI in downstream semantic layers. |
| Medium | Consider explicit unique constraints on natural identifiers such as `customer_id`, `product_id`, `partner_id`, and `rep_id` if business rules require uniqueness. |
| Low | Consider standardizing indicator fields (`is_renewal`, `auto_renew_flag`) to documented controlled vocabularies. |

### Suggested Join Paths

| Use Case | Suggested Join Path |
| --- | --- |
| Fiscal bookings analysis | `fact_bookings` -> `dim_date` |
| Customer segment performance | `fact_bookings` -> `dim_customer` |
| Product family and technology analysis | `fact_bookings` -> `dim_product` |
| Channel and route-to-market analysis | `fact_bookings` -> `dim_partner` |
| Regional performance analysis | `fact_bookings` -> `dim_geography` |
| Sales ownership analysis | `fact_bookings` -> `dim_sales_rep` |
| Contract value and renewal analysis | `fact_bookings` -> `dim_contract` |
| Multi-axis performance analysis | `fact_bookings` joined independently to any combination of all seven dimensions on surrogate keys |

### Data Quality Observations

| Observation | Status | Details |
| --- | --- | --- |
| Row availability | Warning | All tables have 0 rows, so profiling is metadata-only. |
| Referential design | Pass | FK structure is complete and internally consistent. |
| Orphan detection | Limited | Cannot test orphan records without data. |
| Duplicate natural key detection | Limited | Cannot test duplicate `customer_id`, `product_id`, `partner_id`, or `rep_id` without data. |
| Domain value validation | Limited | Cannot validate allowed values for booking and renewal indicators without data. |
| Measure range validation | Limited | Cannot validate booking, ACV, TCV, quantity, or discount ranges without data. |

## Phase 11 Validation Warnings

| Validation Check | Status | Details |
| --- | --- | --- |
| Duplicate entities | Pass | No duplicate entities detected. |
| Duplicate measures | Pass | No duplicate measures detected. |
| Circular relationships | Pass | No circular relationships in explicit FK structure. |
| Missing glossary mappings | Pass | No missing glossary mappings in supplied enriched dictionary. |
| Missing keys | Pass | No missing primary keys; all expected fact-to-dimension foreign keys are present. |
| Orphan entities | Warning | Cannot validate orphan records because all tables are empty. |
| Inferred semantic associations | Warning | Non-FK semantic associations were kept separate and scored below explicit relationships. |
