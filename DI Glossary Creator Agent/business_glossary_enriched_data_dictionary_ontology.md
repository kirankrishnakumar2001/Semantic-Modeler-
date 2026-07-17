# Business Glossary Data Dictionary - ontology

## Step 1 - Input Validation

| Validation Check | Status | Details |
| --- | --- | --- |
| Data Dictionary provided and readable | Pass | PostgreSQL data dictionary for database `ontology` was supplied in prompt context |
| Business context provided and readable | Pass | `Business Domain Context.txt` was read successfully |
| Additional business reference provided and readable | Pass | `Cisco_Bookings_Data_Model_and_Process.docx` was read successfully |
| Profiling reports provided and readable | Pass | Profiling outputs for all 8 tables were supplied in prompt context |
| GitHub credentials provided | Pass | Repository, branch, token, and folder name were supplied |
| GitHub write status | Pass | Markdown output prepared for repository write |

## Step 2 - Business Domain Summary

| Attribute | Value |
| --- | --- |
| Domain Name | Cisco Sales Bookings and Revenue Analytics |
| Modeling Style | Kimball star schema |
| Central Fact Table | `fact_bookings` |
| Grain | One booking transaction / order-line booking event |
| Business Purpose | Analyze bookings performance across customers, products, partners, geography, sales representatives, contracts, and time |
| Primary Measures | Booking Amount, ACV, TCV, Quantity Sold, Unit List Price, Discount Percentage |
| Primary Users | Sales Executives, Regional Sales Managers, Revenue Operations, Finance, Analysts, Partner Teams, Customer Success, Executive Leadership |

## Step 3 - Schema Relationship Summary

| Parent Table | Child Table | Foreign Key Column | Referenced Column | Business Meaning |
| --- | --- | --- | --- | --- |
| `dim_date` | `fact_bookings` | `date_key` | `date_key` | Associates each booking with a reporting and fiscal date |
| `dim_customer` | `fact_bookings` | `customer_key` | `customer_key` | Associates each booking with the customer account |
| `dim_product` | `fact_bookings` | `product_key` | `product_key` | Associates each booking with the sold product or offer |
| `dim_partner` | `fact_bookings` | `partner_key` | `partner_key` | Associates each booking with the partner or channel entity |
| `dim_geography` | `fact_bookings` | `geography_key` | `geography_key` | Associates each booking with sales geography |
| `dim_sales_rep` | `fact_bookings` | `sales_rep_key` | `sales_rep_key` | Associates each booking with the responsible sales representative |
| `dim_contract` | `fact_bookings` | `contract_key` | `contract_key` | Associates each booking with a service or subscription contract context |

## Step 4 - Table Business Glossary

| Table Name | Technical Name | Business Term | Business Definition | Business Description | Business Category | Synonyms | Remarks |
| --- | --- | --- | --- | --- | --- | --- | --- |
| dim_contract | `dim_contract` | Contract Dimension | A dimension table that stores descriptive attributes for customer service, support, or subscription contracts tied to bookings. | Provides contract context such as contract type, term, renewal behavior, and coverage level for bookings analysis. | Contract Management | Contract Master, Agreement Dimension | Empty table in profiling; definitions inferred from schema and business context |
| dim_customer | `dim_customer` | Customer Dimension | A dimension table that stores customer master attributes used to analyze bookings by account, segment, industry, and headquarters geography. | Represents the buying customer in Cisco bookings analytics. | Customer Management | Account Dimension, Customer Master | Empty table in profiling; definitions inferred from schema and business context |
| dim_date | `dim_date` | Date Dimension | A dimension table that stores calendar and fiscal attributes for reporting and time-based analysis. | Enables bookings reporting by date, month, calendar year, and fiscal period. | Time | Calendar Dimension, Time Dimension | Empty table in profiling; definitions inferred from schema and business context |
| dim_geography | `dim_geography` | Geography Dimension | A dimension table that stores regional sales hierarchy attributes used for geographic analysis. | Supports bookings analysis by region, theater, and country. | Geography | Geo Dimension, Sales Geography | Empty table in profiling; definitions inferred from schema and business context |
| dim_partner | `dim_partner` | Partner Dimension | A dimension table that stores partner master data for indirect sales and route-to-market analysis. | Represents distributors, resellers, integrators, and other channel entities participating in bookings. | Channel / Partner | Channel Partner Dimension, Partner Master | Empty table in profiling; definitions inferred from schema and business context |
| dim_product | `dim_product` | Product Dimension | A dimension table that stores product and offer attributes used to analyze product mix and business performance. | Represents Cisco products, subscriptions, and offers across business entities and technology domains. | Product | Offer Dimension, Product Master | Empty table in profiling; definitions inferred from schema and business context |
| dim_sales_rep | `dim_sales_rep` | Sales Representative Dimension | A dimension table that stores sales rep attributes used to analyze bookings ownership and sales performance. | Represents the sales individual and organizational assignment associated with a booking. | Sales | Salesperson Dimension, Rep Dimension | Empty table in profiling; definitions inferred from schema and business context |
| fact_bookings | `fact_bookings` | Booking Transaction Fact | A fact table that stores booking transactions at order-line grain along with commercial measures and dimensional keys. | Central transactional table used to measure bookings demand, renewals, pricing, and contract value. | Sales Transactions | Bookings Fact, Booking Events | Empty table in profiling; fact grain confirmed by schema discovery and business context |

## Step 5 - Enriched Business Glossary Data Dictionary

| Table Name | Column Name | Technical Name | Business Term | Business Definition | Business Description | Data Type | Business Category | Synonyms | Remarks |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| dim_contract | contract_key | `dim_contract.contract_key` | Contract Key | Surrogate key that uniquely identifies a contract record in the contract dimension. | Internal warehouse identifier used to join contract attributes to booking transactions. | integer | Key / Identifier | Contract Surrogate Key | Primary key; no profiling data available because table is empty |
| dim_contract | contract_type | `dim_contract.contract_type` | Contract Type | Type of commercial agreement associated with a booking, such as service, support, or subscription contract. | Classifies the contract model used in Cisco bookings. | character varying(40) | Contract Management | Agreement Type | Business examples referenced in domain material include SmartNet, Enterprise Agreements, Solution Support, and SaaS subscriptions |
| dim_contract | term_months | `dim_contract.term_months` | Contract Term Months | Number of months covered by the contract term. | Indicates the duration of the contract for renewal and value analysis. | integer | Contract Management | Contract Duration Months, Term Length | Useful for ACV and TCV interpretation |
| dim_contract | auto_renew_flag | `dim_contract.auto_renew_flag` | Auto Renewal Indicator | Flag indicating whether the contract is configured to renew automatically. | Supports renewal planning and recurring revenue analysis. | character(1) | Contract Management | Auto Renew Flag, Renewal Flag | Likely coded indicator such as Y/N; no data available to confirm actual domain values |
| dim_contract | coverage_level | `dim_contract.coverage_level` | Coverage Level | Service or support level provided by the contract. | Describes the scope or level of support entitlement attached to the contract. | character varying(20) | Contract Management | Support Level, Service Coverage | Inferred from contract support context |
| dim_customer | customer_key | `dim_customer.customer_key` | Customer Key | Surrogate key that uniquely identifies a customer record in the customer dimension. | Internal warehouse identifier used to join customer attributes to bookings. | integer | Key / Identifier | Customer Surrogate Key | Primary key; no profiling data available because table is empty |
| dim_customer | customer_id | `dim_customer.customer_id` | Customer ID | Business identifier assigned to a customer account. | Stable source-facing customer account identifier distinct from the warehouse surrogate key. | character varying(20) | Customer Management | Account ID, Customer Number | Structurally NOT NULL |
| dim_customer | customer_name | `dim_customer.customer_name` | Customer Name | Official name of the customer account placing the order. | Human-readable customer account name used in reporting and analysis. | character varying(80) | Customer Management | Account Name | Nullable in schema |
| dim_customer | segment | `dim_customer.segment` | Customer Segment | Market segment to which the customer belongs. | Used to analyze bookings across commercial coverage segments. | character varying(30) | Customer Management | Market Segment, Sales Segment | Relevant to coverage and performance analysis |
| dim_customer | industry | `dim_customer.industry` | Industry | Industry classification of the customer account. | Enables industry-based analysis of bookings demand and performance. | character varying(40) | Customer Management | Vertical, Industry Sector | Nullable in schema |
| dim_customer | account_tier | `dim_customer.account_tier` | Account Tier | Tier or strategic ranking assigned to the customer account. | Helps distinguish account priority or service level in business reporting. | character varying(20) | Customer Management | Customer Tier, Account Classification | Inferred from account hierarchy context |
| dim_customer | hq_country | `dim_customer.hq_country` | Headquarters Country | Country where the customer headquarters is located. | Supports customer master geography analysis independent of sales geography. | character varying(40) | Geography / Customer | HQ Country | Nullable in schema |
| dim_customer | hq_region | `dim_customer.hq_region` | Headquarters Region | Region where the customer headquarters is located. | Supports roll-up analysis of customers by headquarters region. | character varying(20) | Geography / Customer | HQ Region | Nullable in schema |
| dim_date | date_key | `dim_date.date_key` | Date Key | Surrogate or encoded key that uniquely identifies a date record in the date dimension. | Join key connecting bookings to calendar and fiscal time attributes. | integer | Key / Identifier | Time Key, Date Surrogate Key | Primary key |
| dim_date | full_date | `dim_date.full_date` | Full Date | The actual calendar date represented by the dimension row. | Base date value used for date-based reporting and reconciliation. | date | Time | Calendar Date | Structurally NOT NULL |
| dim_date | month_name | `dim_date.month_name` | Month Name | Name of the calendar month for the date. | Supports user-friendly month-based reporting. | character varying(12) | Time | Calendar Month Name | Example business values would be January, February, etc.; no data available |
| dim_date | calendar_year | `dim_date.calendar_year` | Calendar Year | Four-digit calendar year of the date. | Used for standard calendar reporting periods. | integer | Time | Year | Nullable in schema |
| dim_date | fiscal_year | `dim_date.fiscal_year` | Fiscal Year | Cisco fiscal year associated with the date. | Supports company-specific fiscal reporting and executive performance analysis. | character varying(6) | Time | FY | Common acronym: FY |
| dim_date | fiscal_quarter | `dim_date.fiscal_quarter` | Fiscal Quarter | Cisco fiscal quarter associated with the date. | Enables reporting aligned to internal quarterly management cycles. | character varying(10) | Time | FQ, Quarter | Common acronym: FQ |
| dim_date | fiscal_period_seq | `dim_date.fiscal_period_seq` | Fiscal Period Sequence | Sequential numeric ordering of fiscal periods. | Supports ordered fiscal time analysis across months or periods. | integer | Time | Fiscal Sequence | Useful for relative time calculations |
| dim_geography | geography_key | `dim_geography.geography_key` | Geography Key | Surrogate key that uniquely identifies a geography record. | Internal warehouse key used to join geography attributes to bookings. | integer | Key / Identifier | Geography Surrogate Key | Primary key |
| dim_geography | region | `dim_geography.region` | Region | Broad sales region associated with the booking or sales coverage model. | Top-level geographic grouping for performance reporting. | character varying(20) | Geography | Sales Region | Nullable in schema |
| dim_geography | theater | `dim_geography.theater` | Theater | Intermediate geography grouping used within Cisco sales organization structures. | Supports organizational roll-ups between region and country. | character varying(30) | Geography | Sales Theater | Cisco-specific geography hierarchy term |
| dim_geography | country | `dim_geography.country` | Country | Country associated with the geography record. | Lowest geography level shown in this schema for country-level reporting. | character varying(40) | Geography | Nation | Nullable in schema |
| dim_partner | partner_key | `dim_partner.partner_key` | Partner Key | Surrogate key that uniquely identifies a partner record in the partner dimension. | Internal warehouse identifier used to join partner data to bookings. | integer | Key / Identifier | Partner Surrogate Key | Primary key |
| dim_partner | partner_id | `dim_partner.partner_id` | Partner ID | Business identifier assigned to a partner organization. | Stable source-facing identifier for a distributor, reseller, or integrator. | character varying(20) | Channel / Partner | Channel Partner ID | Structurally NOT NULL |
| dim_partner | partner_name | `dim_partner.partner_name` | Partner Name | Official name of the partner organization involved in the sale. | Human-readable partner organization name used in channel reporting. | character varying(60) | Channel / Partner | Channel Partner Name | Nullable in schema |
| dim_partner | partner_type | `dim_partner.partner_type` | Partner Type | Classification of partner organization. | Distinguishes categories such as distributor, VAR, reseller, or systems integrator. | character varying(30) | Channel / Partner | Channel Type, Partner Classification | Business context references distributors, VARs, and systems integrators |
| dim_partner | partner_tier | `dim_partner.partner_tier` | Partner Tier | Tier or program level assigned to the partner. | Used to analyze partner performance by certification or strategic level. | character varying(30) | Channel / Partner | Partner Level | Nullable in schema |
| dim_partner | route_to_market | `dim_partner.route_to_market` | Route to Market | Sales route through which the booking was transacted. | Describes whether the booking was sold direct or through indirect channel models. | character varying(20) | Channel / Partner | RTM, Sales Route | Business reference lists direct, two-tier, and reseller routes; common acronym: RTM |
| dim_product | product_key | `dim_product.product_key` | Product Key | Surrogate key that uniquely identifies a product record in the product dimension. | Internal warehouse key used to join product attributes to bookings. | integer | Key / Identifier | Product Surrogate Key | Primary key |
| dim_product | product_id | `dim_product.product_id` | Product ID | Business identifier assigned to a product, SKU, or offer. | Stable identifier used to track product sales across bookings. | character varying(30) | Product | SKU, Offer ID, Product Code | Structurally NOT NULL |
| dim_product | product_name | `dim_product.product_name` | Product Name | Human-readable name of the Cisco product or offer. | Used in reporting to identify the sold item or subscription. | character varying(80) | Product | Offer Name | Nullable in schema |
| dim_product | product_family | `dim_product.product_family` | Product Family | Higher-level grouping of products into common families. | Supports portfolio analysis such as Catalyst, Meraki, Splunk, and similar families. | character varying(30) | Product | Product Portfolio, Family | Reference document mentions product-family mix |
| dim_product | technology_domain | `dim_product.technology_domain` | Technology Domain | Technology area to which the product belongs. | Supports reporting across domains such as networking, security, collaboration, observability, and software. | character varying(40) | Product | Technology Area, Domain | Derived from business context |
| dim_product | offer_type | `dim_product.offer_type` | Offer Type | Commercial offer category for the product. | Distinguishes hardware, software, SaaS, subscription, service, or support offerings. | character varying(30) | Product | Commercial Offer Type | Important for interpreting ACV and TCV applicability |
| dim_product | business_entity | `dim_product.business_entity` | Business Entity | Internal Cisco business unit or portfolio entity associated with the product. | Supports management reporting by business ownership structure. | character varying(30) | Product | Business Unit, Portfolio Entity | Inferred from Cisco portfolio reporting context |
| dim_sales_rep | sales_rep_key | `dim_sales_rep.sales_rep_key` | Sales Representative Key | Surrogate key that uniquely identifies a sales representative record. | Internal warehouse key used to join sales rep attributes to bookings. | integer | Key / Identifier | Sales Rep Surrogate Key | Primary key |
| dim_sales_rep | rep_id | `dim_sales_rep.rep_id` | Sales Representative ID | Business identifier assigned to a sales representative. | Stable identifier for the responsible salesperson or account executive. | character varying(20) | Sales | Rep ID, Employee Sales ID | Structurally NOT NULL |
| dim_sales_rep | rep_name | `dim_sales_rep.rep_name` | Sales Representative Name | Name of the sales representative associated with the booking. | Human-readable salesperson name for performance reporting. | character varying(60) | Sales | Salesperson Name, Account Executive Name | Nullable in schema |
| dim_sales_rep | sales_role | `dim_sales_rep.sales_role` | Sales Role | Role performed by the sales representative in the selling process. | Identifies job function such as account executive or similar sales ownership role. | character varying(40) | Sales | Role, Selling Role | Business process references account executive ownership |
| dim_sales_rep | sales_team | `dim_sales_rep.sales_team` | Sales Team | Organizational sales team to which the representative belongs. | Supports roll-up analysis of performance by team structure. | character varying(40) | Sales | Team, Sales Organization | Nullable in schema |
| dim_sales_rep | segment_covered | `dim_sales_rep.segment_covered` | Segment Covered | Customer segment or market coverage assigned to the sales representative. | Indicates the segment focus of the representative's territory or book of business. | character varying(30) | Sales | Coverage Segment | Nullable in schema |
| fact_bookings | booking_id | `fact_bookings.booking_id` | Booking ID | Unique identifier for a booking transaction record. | Primary key for the fact table at booking transaction or order-line grain. | integer | Key / Identifier | Booking Transaction ID | Primary key |
| fact_bookings | order_number | `fact_bookings.order_number` | Order Number | Customer or partner order number associated with the booking. | Groups one or more booked order lines under the same order transaction. | character varying(20) | Sales Transactions | Sales Order Number, PO Reference | Nullable in schema |
| fact_bookings | order_line_number | `fact_bookings.order_line_number` | Order Line Number | Line item number within the order. | Distinguishes multiple products or services booked under a single order number. | integer | Sales Transactions | Line Number | Fact grain indicates order-line booking event |
| fact_bookings | date_key | `fact_bookings.date_key` | Booking Date Key | Foreign key to the date dimension for the booking event. | Links each booking transaction to calendar and fiscal reporting attributes. | integer | Reference / Time | Booking Time Key | Foreign key to `dim_date.date_key` |
| fact_bookings | customer_key | `fact_bookings.customer_key` | Customer Key | Foreign key to the customer dimension. | Links the booking to the buying customer account. | integer | Reference / Customer | Customer Reference Key | Foreign key to `dim_customer.customer_key` |
| fact_bookings | product_key | `fact_bookings.product_key` | Product Key | Foreign key to the product dimension. | Links the booking to the sold product or commercial offer. | integer | Reference / Product | Product Reference Key | Foreign key to `dim_product.product_key` |
| fact_bookings | partner_key | `fact_bookings.partner_key` | Partner Key | Foreign key to the partner dimension. | Links the booking to the partner involved in the sale, when applicable. | integer | Reference / Channel | Partner Reference Key | Foreign key to `dim_partner.partner_key` |
| fact_bookings | geography_key | `fact_bookings.geography_key` | Geography Key | Foreign key to the geography dimension. | Links the booking to the sales geography used for reporting. | integer | Reference / Geography | Geography Reference Key | Foreign key to `dim_geography.geography_key` |
| fact_bookings | sales_rep_key | `fact_bookings.sales_rep_key` | Sales Representative Key | Foreign key to the sales representative dimension. | Links the booking to the responsible sales owner. | integer | Reference / Sales | Sales Rep Reference Key | Foreign key to `dim_sales_rep.sales_rep_key` |
| fact_bookings | contract_key | `fact_bookings.contract_key` | Contract Key | Foreign key to the contract dimension. | Links the booking to the associated contract or entitlement context. | integer | Reference / Contract | Contract Reference Key | Foreign key to `dim_contract.contract_key` |
| fact_bookings | booking_type | `fact_bookings.booking_type` | Booking Type | Classification of the booking event by commercial motion. | Distinguishes bookings such as New, Renewal, or Upsell. | character varying(15) | Sales Transactions | Booking Classification | Business context explicitly lists New, Renewal, Upsell |
| fact_bookings | is_renewal | `fact_bookings.is_renewal` | Renewal Indicator | Indicator showing whether the booking is related to a contract renewal. | Supports retention and renewal mix analysis. | integer | Sales Transactions | Renewal Flag | Likely binary indicator; schema uses integer and no data is available to confirm coding convention |
| fact_bookings | quantity | `fact_bookings.quantity` | Quantity Sold | Number of units, licenses, or items included in the booking line. | Core volume measure used in product and commercial analysis. | integer | Measures | Units Sold, Quantity | Nullable in schema |
| fact_bookings | unit_list_price_usd | `fact_bookings.unit_list_price_usd` | Unit List Price USD | Standard list price per unit in US dollars before discount. | Baseline unit pricing measure used for discount and margin analysis. | numeric(12,2) | Measures | List Price USD | Currency-denominated measure |
| fact_bookings | discount_pct | `fact_bookings.discount_pct` | Discount Percentage | Percentage discount applied to the list price. | Measures pricing concession level for the booked line. | numeric(5,2) | Measures | Discount Rate, Discount % | Percentage measure |
| fact_bookings | booking_amount_usd | `fact_bookings.booking_amount_usd` | Booking Amount USD | Net booked monetary value in US dollars for the booking line. | Headline demand measure used for bookings reporting and performance tracking. | numeric(14,2) | Measures | Net Bookings USD, Total Booked Value | One of the primary business KPIs |
| fact_bookings | acv_usd | `fact_bookings.acv_usd` | Annual Contract Value USD | Annualized contract value in US dollars associated with the booking. | Key subscription metric used to evaluate recurring annualized value. | numeric(14,2) | Measures | ACV | Common acronym: ACV; reference material notes it is mainly applicable to subscriptions |
| fact_bookings | tcv_usd | `fact_bookings.tcv_usd` | Total Contract Value USD | Total contract value in US dollars associated with the booking. | Measures the full committed contract value across the total contract term. | numeric(14,2) | Measures | TCV | Common acronym: TCV |

## Step 6 - Profiling-Based Remarks

| Table Name | Profiling Observation | Governance Interpretation |
| --- | --- | --- |
| dim_contract | Row count = 0 | Business definitions rely on schema metadata and reference documentation only; no value-domain validation possible |
| dim_customer | Row count = 0 | Customer classifications and hierarchy terms inferred from metadata; no data quality distribution available |
| dim_date | Row count = 0 | Fiscal and calendar attributes structurally present, but no population exists for period validation |
| dim_geography | Row count = 0 | Geography hierarchy definitions inferred; no regional distribution available |
| dim_partner | Row count = 0 | Channel classifications inferred from business context; no partner mix profiling available |
| dim_product | Row count = 0 | Product portfolio terms inferred from business context; no product family distribution available |
| dim_sales_rep | Row count = 0 | Sales ownership attributes structurally defined; no organizational distribution available |
| fact_bookings | Row count = 0 | All commercial measure definitions are metadata-based; no range, completeness, or outlier validation possible |

## Step 7 - Business Glossary Notes

- Definitions were derived from the supplied PostgreSQL schema metadata, profiling reports, `Business Domain Context.txt`, and the Cisco bookings process reference.
- Because all profiled tables currently contain zero rows, glossary descriptions were inferred from structure and domain documentation rather than empirical value distributions.
- Acronyms explicitly supported by business context include `ACV`, `TCV`, `FY`, `FQ`, and `RTM`.
- Surrogate keys were categorized as internal analytical identifiers rather than business-facing identifiers.

## Step 8 - Output Summary

| Metric | Value |
| --- | --- |
| Tables Documented | 8 |
| Columns Documented | 61 |
| Primary Keys Documented | 8 |
| Foreign Keys Documented | 7 |
| Fact Tables | 1 |
| Dimension Tables | 7 |
| Business Domain | Cisco Sales Bookings and Revenue Analytics |
| Output Type | Business Glossary–enriched Data Dictionary |

---

Generated as a business glossary enrichment for PostgreSQL database `ontology` and prepared for storage in the GitHub repository `kirankrishnakumar2001/Semantic-Modeler-` under folder `DI Glossary Creator Agent`.
