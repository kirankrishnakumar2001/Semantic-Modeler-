# OSI Semantic Model

## Domains

| Domain Name | Description |
| --- | --- |
| Sales Bookings | Central transactional domain capturing booking events at order-line grain and the measures used for bookings analytics. |
| Customer | Business domain describing customer accounts, segmentation, industry, and headquarters geography. |
| Product | Business domain describing Cisco products, offers, product families, technology domains, and business entities. |
| Partner / Channel | Business domain describing partner organizations and route-to-market structures for indirect sales analysis. |
| Geography | Business domain describing sales geography hierarchy across region, theater, and country. |
| Sales Organization | Business domain describing sales representatives, roles, teams, and market coverage. |
| Contract | Business domain describing service, support, or subscription contract context tied to bookings. |
| Time | Business domain describing calendar and fiscal reporting attributes. |

## Entities

### Booking Transaction

| Field | Value |
| --- | --- |
| Business Name | Booking Transaction |
| Technical Table Name | `fact_bookings` |
| Description | Central fact table storing booking transactions at one booking transaction / order-line booking event grain with commercial measures and dimensional references. |
| Entity Type | Fact |
| Explicit / Inferred | Explicit |
| Business Keys | `booking_id`; operational grouping fields: `order_number`, `order_line_number` |
| Primary Key | `booking_id` |
| Foreign Keys | `date_key`, `customer_key`, `product_key`, `partner_key`, `geography_key`, `sales_rep_key`, `contract_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Booking ID | `booking_id` | integer | Unique identifier for a booking transaction record. | 1.00 |
| Order Number | `order_number` | character varying(20) | Customer or partner order number associated with the booking. | 0.98 |
| Order Line Number | `order_line_number` | integer | Line item number within the order. | 0.98 |
| Booking Date Key | `date_key` | integer | Foreign key linking the booking to the reporting date. | 1.00 |
| Customer Key | `customer_key` | integer | Foreign key linking the booking to the customer account. | 1.00 |
| Product Key | `product_key` | integer | Foreign key linking the booking to the sold product or offer. | 1.00 |
| Partner Key | `partner_key` | integer | Foreign key linking the booking to the partner involved in the sale. | 1.00 |
| Geography Key | `geography_key` | integer | Foreign key linking the booking to sales geography. | 1.00 |
| Sales Representative Key | `sales_rep_key` | integer | Foreign key linking the booking to the responsible sales representative. | 1.00 |
| Contract Key | `contract_key` | integer | Foreign key linking the booking to associated contract context. | 1.00 |
| Booking Type | `booking_type` | character varying(15) | Classification of the booking event by commercial motion such as New, Renewal, or Upsell. | 0.92 |
| Renewal Indicator | `is_renewal` | integer | Indicator showing whether the booking is related to a contract renewal. | 0.88 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type | Confidence |
| --- | --- | --- | --- | --- | --- |
| Quantity Sold | `quantity` | integer | Number of units, licenses, or items included in the booking line. | Sum | 0.99 |
| Unit List Price USD | `unit_list_price_usd` | numeric(12,2) | Standard list price per unit in US dollars before discount. | Sum, Avg | 0.95 |
| Discount Percentage | `discount_pct` | numeric(5,2) | Percentage discount applied to the list price. | Avg | 0.95 |
| Booking Amount USD | `booking_amount_usd` | numeric(14,2) | Net booked monetary value in US dollars for the booking line. | Sum | 1.00 |
| Annual Contract Value USD | `acv_usd` | numeric(14,2) | Annualized contract value in US dollars associated with the booking. | Sum | 0.97 |
| Total Contract Value USD | `tcv_usd` | numeric(14,2) | Total contract value in US dollars associated with the booking. | Sum | 1.00 |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `booking_id` | Unique fact row identifier |
| Foreign Key | `date_key` | References `dim_date.date_key` |
| Foreign Key | `customer_key` | References `dim_customer.customer_key` |
| Foreign Key | `product_key` | References `dim_product.product_key` |
| Foreign Key | `partner_key` | References `dim_partner.partner_key` |
| Foreign Key | `geography_key` | References `dim_geography.geography_key` |
| Foreign Key | `sales_rep_key` | References `dim_sales_rep.sales_rep_key` |
| Foreign Key | `contract_key` | References `dim_contract.contract_key` |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Booking Transaction occurs on Date | Date | Many-to-One | Many bookings to one date | 1.00 |
| Booking Transaction belongs to Customer | Customer | Many-to-One | Many bookings to one customer | 1.00 |
| Booking Transaction references Product | Product | Many-to-One | Many bookings to one product | 1.00 |
| Booking Transaction references Partner | Partner | Many-to-One | Many bookings to one partner | 1.00 |
| Booking Transaction belongs to Geography | Geography | Many-to-One | Many bookings to one geography | 1.00 |
| Booking Transaction owned by Sales Representative | Sales Representative | Many-to-One | Many bookings to one sales representative | 1.00 |
| Booking Transaction linked to Contract | Contract | Many-to-One | Many bookings to one contract | 1.00 |

---

### Customer

| Field | Value |
| --- | --- |
| Business Name | Customer |
| Technical Table Name | `dim_customer` |
| Description | Customer dimension representing the buying account used for segmentation, industry, and headquarters-based analysis. |
| Entity Type | Dimension |
| Explicit / Inferred | Explicit |
| Business Keys | `customer_id` |
| Primary Key | `customer_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Customer Key | `customer_key` | integer | Surrogate key that uniquely identifies a customer record in the dimension. | 1.00 |
| Customer ID | `customer_id` | character varying(20) | Business identifier assigned to a customer account. | 1.00 |
| Customer Name | `customer_name` | character varying(80) | Official name of the customer account placing the order. | 0.99 |
| Customer Segment | `segment` | character varying(30) | Market segment to which the customer belongs. | 0.98 |
| Industry | `industry` | character varying(40) | Industry classification of the customer account. | 0.99 |
| Account Tier | `account_tier` | character varying(20) | Tier or strategic ranking assigned to the customer account. | 0.93 |
| Headquarters Country | `hq_country` | character varying(40) | Country where the customer headquarters is located. | 0.97 |
| Headquarters Region | `hq_region` | character varying(20) | Region where the customer headquarters is located. | 0.97 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type |
| --- | --- | --- | --- | --- |
| None | N/A | N/A | No explicit measures in this dimension. | N/A |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `customer_key` | Warehouse surrogate key |
| Business Key | `customer_id` | Source-facing customer account identifier |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Customer has Booking Transactions | Booking Transaction | One-to-Many | One customer to many bookings | 1.00 |
| Customer headquarters aligns to Geography context | Geography | Semantic association | Many customers may map to one geography conceptually | 0.55 |

---

### Product

| Field | Value |
| --- | --- |
| Business Name | Product |
| Technical Table Name | `dim_product` |
| Description | Product dimension representing Cisco products, subscriptions, and offers across portfolio and technology domains. |
| Entity Type | Dimension |
| Explicit / Inferred | Explicit |
| Business Keys | `product_id` |
| Primary Key | `product_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Product Key | `product_key` | integer | Surrogate key that uniquely identifies a product record in the dimension. | 1.00 |
| Product ID | `product_id` | character varying(30) | Business identifier assigned to a product, SKU, or offer. | 1.00 |
| Product Name | `product_name` | character varying(80) | Human-readable name of the Cisco product or offer. | 0.99 |
| Product Family | `product_family` | character varying(30) | Higher-level grouping of products into common families. | 0.96 |
| Technology Domain | `technology_domain` | character varying(40) | Technology area to which the product belongs. | 0.97 |
| Offer Type | `offer_type` | character varying(30) | Commercial offer category for the product. | 0.95 |
| Business Entity | `business_entity` | character varying(30) | Internal Cisco business unit or portfolio entity associated with the product. | 0.90 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type |
| --- | --- | --- | --- | --- |
| None | N/A | N/A | No explicit measures in this dimension. | N/A |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `product_key` | Warehouse surrogate key |
| Business Key | `product_id` | Source-facing product/SKU/offer identifier |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Product appears in Booking Transactions | Booking Transaction | One-to-Many | One product to many bookings | 1.00 |
| Product may carry Contract context | Contract | Semantic association | Many products may relate to many contract types conceptually | 0.52 |

---

### Partner

| Field | Value |
| --- | --- |
| Business Name | Partner |
| Technical Table Name | `dim_partner` |
| Description | Partner dimension representing channel organizations participating in indirect sales and route-to-market analysis. |
| Entity Type | Dimension |
| Explicit / Inferred | Explicit |
| Business Keys | `partner_id` |
| Primary Key | `partner_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Partner Key | `partner_key` | integer | Surrogate key that uniquely identifies a partner record in the dimension. | 1.00 |
| Partner ID | `partner_id` | character varying(20) | Business identifier assigned to a partner organization. | 1.00 |
| Partner Name | `partner_name` | character varying(60) | Official name of the partner organization involved in the sale. | 0.99 |
| Partner Type | `partner_type` | character varying(30) | Classification of partner organization. | 0.97 |
| Partner Tier | `partner_tier` | character varying(30) | Tier or program level assigned to the partner. | 0.95 |
| Route to Market | `route_to_market` | character varying(20) | Sales route through which the booking was transacted. | 0.98 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type |
| --- | --- | --- | --- | --- |
| None | N/A | N/A | No explicit measures in this dimension. | N/A |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `partner_key` | Warehouse surrogate key |
| Business Key | `partner_id` | Source-facing partner identifier |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Partner contributes to Booking Transactions | Booking Transaction | One-to-Many | One partner to many bookings | 1.00 |

---

### Geography

| Field | Value |
| --- | --- |
| Business Name | Geography |
| Technical Table Name | `dim_geography` |
| Description | Geography dimension representing the sales geography hierarchy used for regional performance reporting. |
| Entity Type | Dimension |
| Explicit / Inferred | Explicit |
| Business Keys | None explicit beyond descriptive attributes |
| Primary Key | `geography_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Geography Key | `geography_key` | integer | Surrogate key that uniquely identifies a geography record. | 1.00 |
| Region | `region` | character varying(20) | Broad sales region associated with the booking or sales coverage model. | 0.99 |
| Theater | `theater` | character varying(30) | Intermediate geography grouping used within Cisco sales organization structures. | 0.98 |
| Country | `country` | character varying(40) | Country associated with the geography record. | 0.99 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type |
| --- | --- | --- | --- | --- |
| None | N/A | N/A | No explicit measures in this dimension. | N/A |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `geography_key` | Warehouse surrogate key |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Geography contains Booking Transactions | Booking Transaction | One-to-Many | One geography to many bookings | 1.00 |

---

### Sales Representative

| Field | Value |
| --- | --- |
| Business Name | Sales Representative |
| Technical Table Name | `dim_sales_rep` |
| Description | Sales representative dimension representing the sales owner and organizational assignment associated with a booking. |
| Entity Type | Dimension |
| Explicit / Inferred | Explicit |
| Business Keys | `rep_id` |
| Primary Key | `sales_rep_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Sales Representative Key | `sales_rep_key` | integer | Surrogate key that uniquely identifies a sales representative record. | 1.00 |
| Sales Representative ID | `rep_id` | character varying(20) | Business identifier assigned to a sales representative. | 1.00 |
| Sales Representative Name | `rep_name` | character varying(60) | Name of the sales representative associated with the booking. | 0.99 |
| Sales Role | `sales_role` | character varying(40) | Role performed by the sales representative in the selling process. | 0.98 |
| Sales Team | `sales_team` | character varying(40) | Organizational sales team to which the representative belongs. | 0.98 |
| Segment Covered | `segment_covered` | character varying(30) | Customer segment or market coverage assigned to the sales representative. | 0.96 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type |
| --- | --- | --- | --- | --- |
| None | N/A | N/A | No explicit measures in this dimension. | N/A |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `sales_rep_key` | Warehouse surrogate key |
| Business Key | `rep_id` | Source-facing sales representative identifier |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Sales Representative owns Booking Transactions | Booking Transaction | One-to-Many | One sales representative to many bookings | 1.00 |

---

### Contract

| Field | Value |
| --- | --- |
| Business Name | Contract |
| Technical Table Name | `dim_contract` |
| Description | Contract dimension representing service, support, or subscription agreement context associated with bookings. |
| Entity Type | Dimension |
| Explicit / Inferred | Explicit |
| Business Keys | None explicit beyond surrogate key |
| Primary Key | `contract_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Contract Key | `contract_key` | integer | Surrogate key that uniquely identifies a contract record in the dimension. | 1.00 |
| Contract Type | `contract_type` | character varying(40) | Type of commercial agreement associated with a booking, such as service, support, or subscription contract. | 0.97 |
| Contract Term Months | `term_months` | integer | Number of months covered by the contract term. | 0.99 |
| Auto Renewal Indicator | `auto_renew_flag` | character(1) | Flag indicating whether the contract is configured to renew automatically. | 0.90 |
| Coverage Level | `coverage_level` | character varying(20) | Service or support level provided by the contract. | 0.93 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type |
| --- | --- | --- | --- | --- |
| None | N/A | N/A | No explicit measures in this dimension. | N/A |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `contract_key` | Warehouse surrogate key |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Contract applies to Booking Transactions | Booking Transaction | One-to-Many | One contract to many bookings | 1.00 |

---

### Date

| Field | Value |
| --- | --- |
| Business Name | Date |
| Technical Table Name | `dim_date` |
| Description | Date dimension representing calendar and fiscal reporting periods for bookings analysis. |
| Entity Type | Dimension |
| Explicit / Inferred | Explicit |
| Business Keys | `full_date` |
| Primary Key | `date_key` |

#### Attributes

| Attribute Name | Technical Column | Data Type | Business Definition | Glossary Mapping Confidence |
| --- | --- | --- | --- | --- |
| Date Key | `date_key` | integer | Surrogate or encoded key that uniquely identifies a date record. | 1.00 |
| Full Date | `full_date` | date | The actual calendar date represented by the dimension row. | 1.00 |
| Month Name | `month_name` | character varying(12) | Name of the calendar month for the date. | 0.99 |
| Calendar Year | `calendar_year` | integer | Four-digit calendar year of the date. | 0.99 |
| Fiscal Year | `fiscal_year` | character varying(6) | Cisco fiscal year associated with the date. | 0.99 |
| Fiscal Quarter | `fiscal_quarter` | character varying(10) | Cisco fiscal quarter associated with the date. | 0.99 |
| Fiscal Period Sequence | `fiscal_period_seq` | integer | Sequential numeric ordering of fiscal periods. | 0.97 |

#### Measures

| Measure Name | Technical Column | Data Type | Business Definition | Aggregation Type |
| --- | --- | --- | --- | --- |
| None | N/A | N/A | No explicit measures in this dimension. | N/A |

#### Keys

| Key Type | Column | Description |
| --- | --- | --- |
| Primary Key | `date_key` | Warehouse surrogate key |
| Business Key | `full_date` | Calendar date value |

#### Relationships

| Relationship Name | Related Entity | Relationship Type | Cardinality | Confidence Score |
| --- | --- | --- | --- | --- |
| Date organizes Booking Transactions | Booking Transaction | One-to-Many | One date to many bookings | 1.00 |

## Relationships

| Relationship Name | Parent Entity | Child Entity | Relationship Type | Cardinality | Confidence Score | Technical Basis |
| --- | --- | --- | --- | --- | --- | --- |
| Date to Booking Transaction | Date | Booking Transaction | Foreign key / dimensional | One-to-Many | 1.00 | `fact_bookings.date_key -> dim_date.date_key` |
| Customer to Booking Transaction | Customer | Booking Transaction | Foreign key / dimensional | One-to-Many | 1.00 | `fact_bookings.customer_key -> dim_customer.customer_key` |
| Product to Booking Transaction | Product | Booking Transaction | Foreign key / dimensional | One-to-Many | 1.00 | `fact_bookings.product_key -> dim_product.product_key` |
| Partner to Booking Transaction | Partner | Booking Transaction | Foreign key / dimensional | One-to-Many | 1.00 | `fact_bookings.partner_key -> dim_partner.partner_key` |
| Geography to Booking Transaction | Geography | Booking Transaction | Foreign key / dimensional | One-to-Many | 1.00 | `fact_bookings.geography_key -> dim_geography.geography_key` |
| Sales Representative to Booking Transaction | Sales Representative | Booking Transaction | Foreign key / dimensional | One-to-Many | 1.00 | `fact_bookings.sales_rep_key -> dim_sales_rep.sales_rep_key` |
| Contract to Booking Transaction | Contract | Booking Transaction | Foreign key / dimensional | One-to-Many | 1.00 | `fact_bookings.contract_key -> dim_contract.contract_key` |
| Customer Headquarters to Geography | Customer | Geography | Inferred semantic association | Many-to-One inferred | 0.55 | Based on `hq_country` and `hq_region` semantics; no FK |
| Product to Contract Applicability | Product | Contract | Inferred business association | Many-to-Many conceptual | 0.52 | Supported by business process text on support/subscription attachment; no direct FK |

## Measures

| Measure Name | Business Definition | Technical Mapping | Aggregation Type | Notes |
| --- | --- | --- | --- | --- |
| Quantity Sold | Number of units, licenses, or items included in the booking line. | `fact_bookings.quantity` | Sum | Volume measure |
| Unit List Price USD | Standard list price per unit in US dollars before discount. | `fact_bookings.unit_list_price_usd` | Sum, Avg | Best used as Avg for price analysis; Sum available for extended calculations only if semantically intended |
| Discount Percentage | Percentage discount applied to the list price. | `fact_bookings.discount_pct` | Avg | Percentage measure; not typically additive |
| Booking Amount USD | Net booked monetary value in US dollars for the booking line. | `fact_bookings.booking_amount_usd` | Sum | Headline bookings KPI |
| Annual Contract Value USD | Annualized contract value in US dollars associated with the booking. | `fact_bookings.acv_usd` | Sum | Primarily applicable to subscriptions per business process document |
| Total Contract Value USD | Total contract value in US dollars associated with the booking. | `fact_bookings.tcv_usd` | Sum | For subscription and contract-value analysis |

## Glossary Mapping

| Business Term | Technical Mapping | Confidence Score | Preferred Name | Synonyms | Business Domain |
| --- | --- | --- | --- | --- | --- |
| Contract Dimension | `dim_contract` | 0.98 | Contract Dimension | Contract Master; Agreement Dimension | Contract |
| Customer Dimension | `dim_customer` | 0.99 | Customer Dimension | Account Dimension; Customer Master | Customer |
| Date Dimension | `dim_date` | 1.00 | Date Dimension | Calendar Dimension; Time Dimension | Time |
| Geography Dimension | `dim_geography` | 0.99 | Geography Dimension | Geo Dimension; Sales Geography | Geography |
| Partner Dimension | `dim_partner` | 0.99 | Partner Dimension | Channel Partner Dimension; Partner Master | Partner / Channel |
| Product Dimension | `dim_product` | 0.99 | Product Dimension | Offer Dimension; Product Master | Product |
| Sales Representative Dimension | `dim_sales_rep` | 0.99 | Sales Representative Dimension | Salesperson Dimension; Rep Dimension | Sales Organization |
| Booking Transaction Fact | `fact_bookings` | 1.00 | Booking Transaction Fact | Bookings Fact; Booking Events | Sales Bookings |
| Booking Amount USD | `fact_bookings.booking_amount_usd` | 1.00 | Booking Amount USD | Net Bookings USD; Total Booked Value | Sales Bookings |
| Annual Contract Value USD | `fact_bookings.acv_usd` | 0.97 | Annual Contract Value USD | ACV | Sales Bookings |
| Total Contract Value USD | `fact_bookings.tcv_usd` | 1.00 | Total Contract Value USD | TCV | Sales Bookings |
| Quantity Sold | `fact_bookings.quantity` | 0.99 | Quantity Sold | Units Sold; Quantity | Sales Bookings |
| Unit List Price USD | `fact_bookings.unit_list_price_usd` | 0.95 | Unit List Price USD | List Price USD | Sales Bookings |
| Discount Percentage | `fact_bookings.discount_pct` | 0.95 | Discount Percentage | Discount Rate; Discount % | Sales Bookings |
| Booking Type | `fact_bookings.booking_type` | 0.92 | Booking Type | Booking Classification | Sales Bookings |
| Renewal Indicator | `fact_bookings.is_renewal` | 0.88 | Renewal Indicator | Renewal Flag | Sales Bookings |
| Customer ID | `dim_customer.customer_id` | 1.00 | Customer ID | Account ID; Customer Number | Customer |
| Customer Name | `dim_customer.customer_name` | 0.99 | Customer Name | Account Name | Customer |
| Customer Segment | `dim_customer.segment` | 0.98 | Customer Segment | Market Segment; Sales Segment | Customer |
| Industry | `dim_customer.industry` | 0.99 | Industry | Vertical; Industry Sector | Customer |
| Account Tier | `dim_customer.account_tier` | 0.93 | Account Tier | Customer Tier; Account Classification | Customer |
| Headquarters Country | `dim_customer.hq_country` | 0.97 | Headquarters Country | HQ Country | Customer |
| Headquarters Region | `dim_customer.hq_region` | 0.97 | Headquarters Region | HQ Region | Customer |
| Product ID | `dim_product.product_id` | 1.00 | Product ID | SKU; Offer ID; Product Code | Product |
| Product Name | `dim_product.product_name` | 0.99 | Product Name | Offer Name | Product |
| Product Family | `dim_product.product_family` | 0.96 | Product Family | Product Portfolio; Family | Product |
| Technology Domain | `dim_product.technology_domain` | 0.97 | Technology Domain | Technology Area; Domain | Product |
| Offer Type | `dim_product.offer_type` | 0.95 | Offer Type | Commercial Offer Type | Product |
| Business Entity | `dim_product.business_entity` | 0.90 | Business Entity | Business Unit; Portfolio Entity | Product |
| Partner ID | `dim_partner.partner_id` | 1.00 | Partner ID | Channel Partner ID | Partner / Channel |
| Partner Name | `dim_partner.partner_name` | 0.99 | Partner Name | Channel Partner Name | Partner / Channel |
| Partner Type | `dim_partner.partner_type` | 0.97 | Partner Type | Channel Type; Partner Classification | Partner / Channel |
| Partner Tier | `dim_partner.partner_tier` | 0.95 | Partner Tier | Partner Level | Partner / Channel |
| Route to Market | `dim_partner.route_to_market` | 0.98 | Route to Market | RTM; Sales Route | Partner / Channel |
| Region | `dim_geography.region` | 0.99 | Region | Sales Region | Geography |
| Theater | `dim_geography.theater` | 0.98 | Theater | Sales Theater | Geography |
| Country | `dim_geography.country` | 0.99 | Country | Nation | Geography |
| Sales Representative ID | `dim_sales_rep.rep_id` | 1.00 | Sales Representative ID | Rep ID; Employee Sales ID | Sales Organization |
| Sales Representative Name | `dim_sales_rep.rep_name` | 0.99 | Sales Representative Name | Salesperson Name; Account Executive Name | Sales Organization |
| Sales Role | `dim_sales_rep.sales_role` | 0.98 | Sales Role | Role; Selling Role | Sales Organization |
| Sales Team | `dim_sales_rep.sales_team` | 0.98 | Sales Team | Team; Sales Organization | Sales Organization |
| Segment Covered | `dim_sales_rep.segment_covered` | 0.96 | Segment Covered | Coverage Segment | Sales Organization |
| Contract Type | `dim_contract.contract_type` | 0.97 | Contract Type | Agreement Type | Contract |
| Contract Term Months | `dim_contract.term_months` | 0.99 | Contract Term Months | Contract Duration Months; Term Length | Contract |
| Auto Renewal Indicator | `dim_contract.auto_renew_flag` | 0.90 | Auto Renewal Indicator | Auto Renew Flag; Renewal Flag | Contract |
| Coverage Level | `dim_contract.coverage_level` | 0.93 | Coverage Level | Support Level; Service Coverage | Contract |
| Full Date | `dim_date.full_date` | 1.00 | Full Date | Calendar Date | Time |
| Month Name | `dim_date.month_name` | 0.99 | Month Name | Calendar Month Name | Time |
| Calendar Year | `dim_date.calendar_year` | 0.99 | Calendar Year | Year | Time |
| Fiscal Year | `dim_date.fiscal_year` | 0.99 | Fiscal Year | FY | Time |
| Fiscal Quarter | `dim_date.fiscal_quarter` | 0.99 | Fiscal Quarter | FQ; Quarter | Time |
| Fiscal Period Sequence | `dim_date.fiscal_period_seq` | 0.97 | Fiscal Period Sequence | Fiscal Sequence | Time |

## Validation

| Validation Check | Status | Details |
| --- | --- | --- |
| Duplicate entities | Pass | No duplicate entities detected across the semantic model. |
| Duplicate measures | Pass | No duplicate measures detected. |
| Circular relationships | Pass | No circular relationships found in the explicit FK graph. |
| Missing glossary mappings | Pass | All modeled tables and columns are represented in supplied glossary content. |
| Missing keys | Pass | All tables have primary keys and the fact has all documented dimensional foreign keys. |
| Orphan entities | Warning | Orphan record validation cannot be performed because all tables are empty. |
| Data-backed semantic validation | Warning | Value-domain and measure-behavior validation is limited because row count is 0 for all tables. |
| Inferred content control | Pass | Inferred items are clearly labeled and confidence-scored; no unsupported entities or physical relationships were invented. |
