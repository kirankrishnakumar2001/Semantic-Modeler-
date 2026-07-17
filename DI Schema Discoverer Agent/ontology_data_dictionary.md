# PostgreSQL Data Dictionary - ontology

## Step 1 - Input Validation

| Validation Check | Status | Details |
| --- | --- | --- |
| Database credentials complete | Pass | Connection executed successfully via provided PostgreSQL query runner tool context |
| Required connection parameters present | Pass | Database context resolved successfully |
| Database type supported | Pass | PostgreSQL 16.14 |
| Output format valid | Pass | Markdown generated |

## Step 2 - Secure Connection and Connectivity Validation

| Item | Value |
| --- | --- |
| Database Name | ontology |
| Database Version | PostgreSQL 16.14 on x86_64-pc-linux-gnu, compiled by gcc (GCC) 13.2.0, 64-bit |
| Current User | ontologyuser1 |
| Connectivity Status | Success |
| Supported Platform | PostgreSQL |

## Step 3 - Schema Discovery

| Schema Name |
| --- |
| ontology |
| public |

> System schemas `information_schema` and `pg_catalog` were excluded from business metadata normalization.

## Business Domain Context

**Domain Name:** Cisco Sales Bookings and Revenue Analytics

This database represents Cisco sales booking operations for enterprise networking, security, collaboration, observability, and software subscription products. The model follows a Kimball star schema where `fact_bookings` stores booking transactions and surrounding dimension tables provide customer, product, partner, geography, sales representative, contract, and date context.

## Step 4 - Structural Metadata

### Tables

| Database Name | Schema | Table Name | Owner | Table Type | Description |
| --- | --- | --- | --- | --- | --- |
| ontology | ontology | dim_contract | ontologyuser1 | BASE TABLE |  |
| ontology | ontology | dim_customer | ontologyuser1 | BASE TABLE |  |
| ontology | ontology | dim_date | ontologyuser1 | BASE TABLE |  |
| ontology | ontology | dim_geography | ontologyuser1 | BASE TABLE |  |
| ontology | ontology | dim_partner | ontologyuser1 | BASE TABLE |  |
| ontology | ontology | dim_product | ontologyuser1 | BASE TABLE |  |
| ontology | ontology | dim_sales_rep | ontologyuser1 | BASE TABLE |  |
| ontology | ontology | fact_bookings | ontologyuser1 | BASE TABLE |  |

### Normalized Column Metadata

| Database Name | Schema | Table Name | Object Type | Column Name | Data Type | Length | Precision | Scale | Nullable | Default Value | Identity/Auto Increment | Primary Key | Foreign Key | Referenced Table | Referenced Column | Index | Constraint | Description/Remarks | DDL Statement |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ontology | ontology | dim_contract | TABLE | contract_key | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | dim_contract_pkey | dim_contract_pkey |  | `contract_key integer NOT NULL` |
| ontology | ontology | dim_contract | TABLE | contract_type | character varying | 40 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `contract_type character varying(40)` |
| ontology | ontology | dim_contract | TABLE | term_months | integer |  | 32 | 0 | YES |  | NO | NO | NO |  |  |  |  |  | `term_months integer` |
| ontology | ontology | dim_contract | TABLE | auto_renew_flag | character | 1 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `auto_renew_flag character(1)` |
| ontology | ontology | dim_contract | TABLE | coverage_level | character varying | 20 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `coverage_level character varying(20)` |
| ontology | ontology | dim_customer | TABLE | customer_key | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | dim_customer_pkey | dim_customer_pkey |  | `customer_key integer NOT NULL` |
| ontology | ontology | dim_customer | TABLE | customer_id | character varying | 20 |  |  | NO |  | NO | NO | NO |  |  |  |  |  | `customer_id character varying(20) NOT NULL` |
| ontology | ontology | dim_customer | TABLE | customer_name | character varying | 80 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `customer_name character varying(80)` |
| ontology | ontology | dim_customer | TABLE | segment | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `segment character varying(30)` |
| ontology | ontology | dim_customer | TABLE | industry | character varying | 40 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `industry character varying(40)` |
| ontology | ontology | dim_customer | TABLE | account_tier | character varying | 20 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `account_tier character varying(20)` |
| ontology | ontology | dim_customer | TABLE | hq_country | character varying | 40 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `hq_country character varying(40)` |
| ontology | ontology | dim_customer | TABLE | hq_region | character varying | 20 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `hq_region character varying(20)` |
| ontology | ontology | dim_date | TABLE | date_key | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | dim_date_pkey | dim_date_pkey |  | `date_key integer NOT NULL` |
| ontology | ontology | dim_date | TABLE | full_date | date |  |  |  | NO |  | NO | NO | NO |  |  |  |  |  | `full_date date NOT NULL` |
| ontology | ontology | dim_date | TABLE | month_name | character varying | 12 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `month_name character varying(12)` |
| ontology | ontology | dim_date | TABLE | calendar_year | integer |  | 32 | 0 | YES |  | NO | NO | NO |  |  |  |  |  | `calendar_year integer` |
| ontology | ontology | dim_date | TABLE | fiscal_year | character varying | 6 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `fiscal_year character varying(6)` |
| ontology | ontology | dim_date | TABLE | fiscal_quarter | character varying | 10 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `fiscal_quarter character varying(10)` |
| ontology | ontology | dim_date | TABLE | fiscal_period_seq | integer |  | 32 | 0 | YES |  | NO | NO | NO |  |  |  |  |  | `fiscal_period_seq integer` |
| ontology | ontology | dim_geography | TABLE | geography_key | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | dim_geography_pkey | dim_geography_pkey |  | `geography_key integer NOT NULL` |
| ontology | ontology | dim_geography | TABLE | region | character varying | 20 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `region character varying(20)` |
| ontology | ontology | dim_geography | TABLE | theater | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `theater character varying(30)` |
| ontology | ontology | dim_geography | TABLE | country | character varying | 40 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `country character varying(40)` |
| ontology | ontology | dim_partner | TABLE | partner_key | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | dim_partner_pkey | dim_partner_pkey |  | `partner_key integer NOT NULL` |
| ontology | ontology | dim_partner | TABLE | partner_id | character varying | 20 |  |  | NO |  | NO | NO | NO |  |  |  |  |  | `partner_id character varying(20) NOT NULL` |
| ontology | ontology | dim_partner | TABLE | partner_name | character varying | 60 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `partner_name character varying(60)` |
| ontology | ontology | dim_partner | TABLE | partner_type | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `partner_type character varying(30)` |
| ontology | ontology | dim_partner | TABLE | partner_tier | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `partner_tier character varying(30)` |
| ontology | ontology | dim_partner | TABLE | route_to_market | character varying | 20 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `route_to_market character varying(20)` |
| ontology | ontology | dim_product | TABLE | product_key | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | dim_product_pkey | dim_product_pkey |  | `product_key integer NOT NULL` |
| ontology | ontology | dim_product | TABLE | product_id | character varying | 30 |  |  | NO |  | NO | NO | NO |  |  |  |  |  | `product_id character varying(30) NOT NULL` |
| ontology | ontology | dim_product | TABLE | product_name | character varying | 80 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `product_name character varying(80)` |
| ontology | ontology | dim_product | TABLE | product_family | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `product_family character varying(30)` |
| ontology | ontology | dim_product | TABLE | technology_domain | character varying | 40 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `technology_domain character varying(40)` |
| ontology | ontology | dim_product | TABLE | offer_type | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `offer_type character varying(30)` |
| ontology | ontology | dim_product | TABLE | business_entity | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `business_entity character varying(30)` |
| ontology | ontology | dim_sales_rep | TABLE | sales_rep_key | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | dim_sales_rep_pkey | dim_sales_rep_pkey |  | `sales_rep_key integer NOT NULL` |
| ontology | ontology | dim_sales_rep | TABLE | rep_id | character varying | 20 |  |  | NO |  | NO | NO | NO |  |  |  |  |  | `rep_id character varying(20) NOT NULL` |
| ontology | ontology | dim_sales_rep | TABLE | rep_name | character varying | 60 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `rep_name character varying(60)` |
| ontology | ontology | dim_sales_rep | TABLE | sales_role | character varying | 40 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `sales_role character varying(40)` |
| ontology | ontology | dim_sales_rep | TABLE | sales_team | character varying | 40 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `sales_team character varying(40)` |
| ontology | ontology | dim_sales_rep | TABLE | segment_covered | character varying | 30 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `segment_covered character varying(30)` |
| ontology | ontology | fact_bookings | TABLE | booking_id | integer |  | 32 | 0 | NO |  | NO | YES | NO |  |  | fact_bookings_pkey | fact_bookings_pkey |  | `booking_id integer NOT NULL` |
| ontology | ontology | fact_bookings | TABLE | order_number | character varying | 20 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `order_number character varying(20)` |
| ontology | ontology | fact_bookings | TABLE | order_line_number | integer |  | 32 | 0 | YES |  | NO | NO | NO |  |  |  |  |  | `order_line_number integer` |
| ontology | ontology | fact_bookings | TABLE | date_key | integer |  | 32 | 0 | YES |  | NO | NO | YES | dim_date | date_key |  | fk_booking_date |  | `date_key integer` |
| ontology | ontology | fact_bookings | TABLE | customer_key | integer |  | 32 | 0 | YES |  | NO | NO | YES | dim_customer | customer_key |  | fk_booking_customer |  | `customer_key integer` |
| ontology | ontology | fact_bookings | TABLE | product_key | integer |  | 32 | 0 | YES |  | NO | NO | YES | dim_product | product_key |  | fk_booking_product |  | `product_key integer` |
| ontology | ontology | fact_bookings | TABLE | partner_key | integer |  | 32 | 0 | YES |  | NO | NO | YES | dim_partner | partner_key |  | fk_booking_partner |  | `partner_key integer` |
| ontology | ontology | fact_bookings | TABLE | geography_key | integer |  | 32 | 0 | YES |  | NO | NO | YES | dim_geography | geography_key |  | fk_booking_geography |  | `geography_key integer` |
| ontology | ontology | fact_bookings | TABLE | sales_rep_key | integer |  | 32 | 0 | YES |  | NO | NO | YES | dim_sales_rep | sales_rep_key |  | fk_booking_sales_rep |  | `sales_rep_key integer` |
| ontology | ontology | fact_bookings | TABLE | contract_key | integer |  | 32 | 0 | YES |  | NO | NO | YES | dim_contract | contract_key |  | fk_booking_contract |  | `contract_key integer` |
| ontology | ontology | fact_bookings | TABLE | booking_type | character varying | 15 |  |  | YES |  | NO | NO | NO |  |  |  |  |  | `booking_type character varying(15)` |
| ontology | ontology | fact_bookings | TABLE | is_renewal | integer |  | 32 | 0 | YES |  | NO | NO | NO |  |  |  |  |  | `is_renewal integer` |
| ontology | ontology | fact_bookings | TABLE | quantity | integer |  | 32 | 0 | YES |  | NO | NO | NO |  |  |  |  |  | `quantity integer` |
| ontology | ontology | fact_bookings | TABLE | unit_list_price_usd | numeric |  | 12 | 2 | YES |  | NO | NO | NO |  |  |  |  |  | `unit_list_price_usd numeric(12,2)` |
| ontology | ontology | fact_bookings | TABLE | discount_pct | numeric |  | 5 | 2 | YES |  | NO | NO | NO |  |  |  |  |  | `discount_pct numeric(5,2)` |
| ontology | ontology | fact_bookings | TABLE | booking_amount_usd | numeric |  | 14 | 2 | YES |  | NO | NO | NO |  |  |  |  |  | `booking_amount_usd numeric(14,2)` |
| ontology | ontology | fact_bookings | TABLE | acv_usd | numeric |  | 14 | 2 | YES |  | NO | NO | NO |  |  |  |  |  | `acv_usd numeric(14,2)` |
| ontology | ontology | fact_bookings | TABLE | tcv_usd | numeric |  | 14 | 2 | YES |  | NO | NO | NO |  |  |  |  |  | `tcv_usd numeric(14,2)` |

### Primary Keys

| Schema | Table Name | Primary Key Column |
| --- | --- | --- |
| ontology | dim_contract | contract_key |
| ontology | dim_customer | customer_key |
| ontology | dim_date | date_key |
| ontology | dim_geography | geography_key |
| ontology | dim_partner | partner_key |
| ontology | dim_product | product_key |
| ontology | dim_sales_rep | sales_rep_key |
| ontology | fact_bookings | booking_id |

### Foreign Keys / Relationships

| Parent Table | Child Table | Foreign Key Column | Referenced Column | Constraint Name |
| --- | --- | --- | --- | --- |
| dim_contract | fact_bookings | contract_key | contract_key | fk_booking_contract |
| dim_customer | fact_bookings | customer_key | customer_key | fk_booking_customer |
| dim_date | fact_bookings | date_key | date_key | fk_booking_date |
| dim_geography | fact_bookings | geography_key | geography_key | fk_booking_geography |
| dim_partner | fact_bookings | partner_key | partner_key | fk_booking_partner |
| dim_product | fact_bookings | product_key | product_key | fk_booking_product |
| dim_sales_rep | fact_bookings | sales_rep_key | sales_rep_key | fk_booking_sales_rep |

### Constraints

| Schema | Table Name | Constraint Name | Constraint Type | Constraint Definition |
| --- | --- | --- | --- | --- |
| ontology | dim_contract | dim_contract_pkey | PRIMARY KEY | PRIMARY KEY (contract_key) |
| ontology | dim_customer | dim_customer_pkey | PRIMARY KEY | PRIMARY KEY (customer_key) |
| ontology | dim_date | dim_date_pkey | PRIMARY KEY | PRIMARY KEY (date_key) |
| ontology | dim_geography | dim_geography_pkey | PRIMARY KEY | PRIMARY KEY (geography_key) |
| ontology | dim_partner | dim_partner_pkey | PRIMARY KEY | PRIMARY KEY (partner_key) |
| ontology | dim_product | dim_product_pkey | PRIMARY KEY | PRIMARY KEY (product_key) |
| ontology | dim_sales_rep | dim_sales_rep_pkey | PRIMARY KEY | PRIMARY KEY (sales_rep_key) |
| ontology | fact_bookings | fact_bookings_pkey | PRIMARY KEY | PRIMARY KEY (booking_id) |
| ontology | fact_bookings | fk_booking_contract | FOREIGN KEY | FOREIGN KEY (contract_key) REFERENCES dim_contract(contract_key) |
| ontology | fact_bookings | fk_booking_customer | FOREIGN KEY | FOREIGN KEY (customer_key) REFERENCES dim_customer(customer_key) |
| ontology | fact_bookings | fk_booking_date | FOREIGN KEY | FOREIGN KEY (date_key) REFERENCES dim_date(date_key) |
| ontology | fact_bookings | fk_booking_geography | FOREIGN KEY | FOREIGN KEY (geography_key) REFERENCES dim_geography(geography_key) |
| ontology | fact_bookings | fk_booking_partner | FOREIGN KEY | FOREIGN KEY (partner_key) REFERENCES dim_partner(partner_key) |
| ontology | fact_bookings | fk_booking_product | FOREIGN KEY | FOREIGN KEY (product_key) REFERENCES dim_product(product_key) |
| ontology | fact_bookings | fk_booking_sales_rep | FOREIGN KEY | FOREIGN KEY (sales_rep_key) REFERENCES dim_sales_rep(sales_rep_key) |

### Indexes

| Schema | Table Name | Index Name | Indexed Columns | Index Type | Uniqueness | Index DDL |
| --- | --- | --- | --- | --- | --- | --- |
| ontology | dim_contract | dim_contract_pkey | contract_key | btree | UNIQUE | `CREATE UNIQUE INDEX dim_contract_pkey ON ontology.dim_contract USING btree (contract_key)` |
| ontology | dim_customer | dim_customer_pkey | customer_key | btree | UNIQUE | `CREATE UNIQUE INDEX dim_customer_pkey ON ontology.dim_customer USING btree (customer_key)` |
| ontology | dim_date | dim_date_pkey | date_key | btree | UNIQUE | `CREATE UNIQUE INDEX dim_date_pkey ON ontology.dim_date USING btree (date_key)` |
| ontology | dim_geography | dim_geography_pkey | geography_key | btree | UNIQUE | `CREATE UNIQUE INDEX dim_geography_pkey ON ontology.dim_geography USING btree (geography_key)` |
| ontology | dim_partner | dim_partner_pkey | partner_key | btree | UNIQUE | `CREATE UNIQUE INDEX dim_partner_pkey ON ontology.dim_partner USING btree (partner_key)` |
| ontology | dim_product | dim_product_pkey | product_key | btree | UNIQUE | `CREATE UNIQUE INDEX dim_product_pkey ON ontology.dim_product USING btree (product_key)` |
| ontology | dim_sales_rep | dim_sales_rep_pkey | sales_rep_key | btree | UNIQUE | `CREATE UNIQUE INDEX dim_sales_rep_pkey ON ontology.dim_sales_rep USING btree (sales_rep_key)` |
| ontology | fact_bookings | fact_bookings_pkey | booking_id | btree | UNIQUE | `CREATE UNIQUE INDEX fact_bookings_pkey ON ontology.fact_bookings USING btree (booking_id)` |

### Database Objects Summary

| Object Type | Count | Notes |
| --- | --- | --- |
| Tables | 8 | All discovered in schema `ontology` |
| Views | 0 | None discovered |
| Materialized Views | 0 | None discovered |
| Sequences | 0 | None discovered |
| Stored Procedures | 0 | None discovered |
| Functions | 0 | None discovered |
| Triggers | 0 | None discovered |
| Partitioned Tables | 0 | None discovered |

## Step 5 - DDL Extraction

### Table DDL

#### ontology.dim_contract
```sql
CREATE TABLE ontology.dim_contract (
    contract_key integer NOT NULL,
    contract_type character varying(40),
    term_months integer,
    auto_renew_flag character(1),
    coverage_level character varying(20)
);
```

#### ontology.dim_customer
```sql
CREATE TABLE ontology.dim_customer (
    customer_key integer NOT NULL,
    customer_id character varying(20) NOT NULL,
    customer_name character varying(80),
    segment character varying(30),
    industry character varying(40),
    account_tier character varying(20),
    hq_country character varying(40),
    hq_region character varying(20)
);
```

#### ontology.dim_date
```sql
CREATE TABLE ontology.dim_date (
    date_key integer NOT NULL,
    full_date date NOT NULL,
    month_name character varying(12),
    calendar_year integer,
    fiscal_year character varying(6),
    fiscal_quarter character varying(10),
    fiscal_period_seq integer
);
```

#### ontology.dim_geography
```sql
CREATE TABLE ontology.dim_geography (
    geography_key integer NOT NULL,
    region character varying(20),
    theater character varying(30),
    country character varying(40)
);
```

#### ontology.dim_partner
```sql
CREATE TABLE ontology.dim_partner (
    partner_key integer NOT NULL,
    partner_id character varying(20) NOT NULL,
    partner_name character varying(60),
    partner_type character varying(30),
    partner_tier character varying(30),
    route_to_market character varying(20)
);
```

#### ontology.dim_product
```sql
CREATE TABLE ontology.dim_product (
    product_key integer NOT NULL,
    product_id character varying(30) NOT NULL,
    product_name character varying(80),
    product_family character varying(30),
    technology_domain character varying(40),
    offer_type character varying(30),
    business_entity character varying(30)
);
```

#### ontology.dim_sales_rep
```sql
CREATE TABLE ontology.dim_sales_rep (
    sales_rep_key integer NOT NULL,
    rep_id character varying(20) NOT NULL,
    rep_name character varying(60),
    sales_role character varying(40),
    sales_team character varying(40),
    segment_covered character varying(30)
);
```

#### ontology.fact_bookings
```sql
CREATE TABLE ontology.fact_bookings (
    booking_id integer NOT NULL,
    order_number character varying(20),
    order_line_number integer,
    date_key integer,
    customer_key integer,
    product_key integer,
    partner_key integer,
    geography_key integer,
    sales_rep_key integer,
    contract_key integer,
    booking_type character varying(15),
    is_renewal integer,
    quantity integer,
    unit_list_price_usd numeric(12,2),
    discount_pct numeric(5,2),
    booking_amount_usd numeric(14,2),
    acv_usd numeric(14,2),
    tcv_usd numeric(14,2)
);
```

### Constraint DDL

```sql
ALTER TABLE ontology.dim_contract ADD CONSTRAINT dim_contract_pkey PRIMARY KEY (contract_key);
ALTER TABLE ontology.dim_customer ADD CONSTRAINT dim_customer_pkey PRIMARY KEY (customer_key);
ALTER TABLE ontology.dim_date ADD CONSTRAINT dim_date_pkey PRIMARY KEY (date_key);
ALTER TABLE ontology.dim_geography ADD CONSTRAINT dim_geography_pkey PRIMARY KEY (geography_key);
ALTER TABLE ontology.dim_partner ADD CONSTRAINT dim_partner_pkey PRIMARY KEY (partner_key);
ALTER TABLE ontology.dim_product ADD CONSTRAINT dim_product_pkey PRIMARY KEY (product_key);
ALTER TABLE ontology.dim_sales_rep ADD CONSTRAINT dim_sales_rep_pkey PRIMARY KEY (sales_rep_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fact_bookings_pkey PRIMARY KEY (booking_id);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_contract FOREIGN KEY (contract_key) REFERENCES dim_contract(contract_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_customer FOREIGN KEY (customer_key) REFERENCES dim_customer(customer_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_date FOREIGN KEY (date_key) REFERENCES dim_date(date_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_geography FOREIGN KEY (geography_key) REFERENCES dim_geography(geography_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_partner FOREIGN KEY (partner_key) REFERENCES dim_partner(partner_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_product FOREIGN KEY (product_key) REFERENCES dim_product(product_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_sales_rep FOREIGN KEY (sales_rep_key) REFERENCES dim_sales_rep(sales_rep_key);
```

### Index DDL

```sql
CREATE UNIQUE INDEX dim_contract_pkey ON ontology.dim_contract USING btree (contract_key);
CREATE UNIQUE INDEX dim_customer_pkey ON ontology.dim_customer USING btree (customer_key);
CREATE UNIQUE INDEX dim_date_pkey ON ontology.dim_date USING btree (date_key);
CREATE UNIQUE INDEX dim_geography_pkey ON ontology.dim_geography USING btree (geography_key);
CREATE UNIQUE INDEX dim_partner_pkey ON ontology.dim_partner USING btree (partner_key);
CREATE UNIQUE INDEX dim_product_pkey ON ontology.dim_product USING btree (product_key);
CREATE UNIQUE INDEX dim_sales_rep_pkey ON ontology.dim_sales_rep USING btree (sales_rep_key);
CREATE UNIQUE INDEX fact_bookings_pkey ON ontology.fact_bookings USING btree (booking_id);
```

## Step 6 - Normalization Notes

| Normalization Rule | Applied |
| --- | --- |
| Common object naming fields used | Yes |
| Consistent object type labels used | Yes |
| Length, precision, scale split into separate columns | Yes |
| PK/FK flags normalized to YES/NO | Yes |
| DDL grouped by object type | Yes |
| System schemas excluded from business dictionary | Yes |

## Step 7 - Metadata Completeness Validation

| Validation Rule | Status | Details |
| --- | --- | --- |
| Every discovered table has associated column metadata | Pass | 8/8 tables covered |
| Primary keys identified | Pass | 8 tables with PKs |
| Foreign key relationships identified | Pass | 7 FK relationships from fact to dimensions |
| Object names unique within schema | Pass | No duplicates found in discovered business objects |
| DDL extraction completed where supported | Partial Pass | Table, constraint, and index DDL extracted; no views, sequences, functions, procedures, or triggers existed |
| Missing metadata reported | Pass | No descriptions/remarks populated in source catalog |

## Step 8 - Standardized Data Dictionary Summary

| Metric | Value |
| --- | --- |
| Database Name | ontology |
| Database Version | PostgreSQL 16.14 |
| Business Schema Count | 1 |
| Business Tables | 8 |
| Total Columns | 61 |
| Primary Keys | 8 |
| Foreign Keys | 7 |
| Indexes | 8 |
| Views | 0 |
| Functions | 0 |
| Procedures | 0 |
| Triggers | 0 |
| Sequences | 0 |

## Semantic Modeling Observations

| Subject Area | Observation |
| --- | --- |
| Modeling Style | Kimball star schema |
| Central Fact | `fact_bookings` |
| Dimensions | `dim_customer`, `dim_product`, `dim_partner`, `dim_geography`, `dim_sales_rep`, `dim_contract`, `dim_date` |
| Grain | One booking transaction / order line booking event |
| Main Measures | `booking_amount_usd`, `acv_usd`, `tcv_usd`, `quantity`, `unit_list_price_usd`, `discount_pct` |
| Business Utility | Enterprise documentation, governance, cataloging, semantic modeling, ontology generation, AI metadata discovery |

## Missing / Not Available Metadata

| Metadata Category | Status |
| --- | --- |
| Table comments | Not available |
| Column comments | Not available |
| Unique constraints beyond PK indexes | Not found |
| Check constraints beyond system-generated not-null artifacts | Not captured in normalized business dictionary |
| Views | Not found |
| Stored procedures | Not found |
| Functions | Not found |
| Triggers | Not found |
| Sequences | Not found |

---
Generated from PostgreSQL system catalog discovery and normalized for platform-independent data dictionary use.
