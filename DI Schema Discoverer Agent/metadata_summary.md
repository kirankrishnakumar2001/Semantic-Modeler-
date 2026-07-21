# Metadata Summary

## Source System Identification
- **Database Platform:** PostgreSQL
- **Database Name:** ontology
- **Current Schema:** ontology
- **Database Version:** PostgreSQL 16.14
- **Schema Owner / Query User:** ontologyuser1

## Step 3 – Database-Specific Metadata SQL
The following PostgreSQL-specific SQL statements were generated and used to discover metadata from system catalogs and the information schema.

### 1. Platform Identification
```sql
SELECT current_database() AS database_name,
       current_schema() AS current_schema,
       version() AS version,
       current_user AS current_user;
```

### 2. Table Discovery
```sql
SELECT table_schema,
       table_name,
       table_type
FROM information_schema.tables
WHERE table_schema NOT IN ('pg_catalog','information_schema')
ORDER BY table_schema, table_name;
```

### 3. Column Discovery
```sql
SELECT table_schema,
       table_name,
       column_name,
       ordinal_position,
       data_type,
       udt_name,
       is_nullable,
       column_default,
       character_maximum_length,
       numeric_precision,
       numeric_scale
FROM information_schema.columns
WHERE table_schema NOT IN ('pg_catalog','information_schema')
ORDER BY table_schema, table_name, ordinal_position;
```

### 4. Constraints and Relationships Discovery
```sql
SELECT tc.table_schema,
       tc.table_name,
       tc.constraint_name,
       tc.constraint_type,
       kcu.column_name,
       ccu.table_schema AS foreign_table_schema,
       ccu.table_name AS foreign_table_name,
       ccu.column_name AS foreign_column_name
FROM information_schema.table_constraints tc
LEFT JOIN information_schema.key_column_usage kcu
  ON tc.constraint_name = kcu.constraint_name
 AND tc.table_schema = kcu.table_schema
 AND tc.table_name = kcu.table_name
LEFT JOIN information_schema.constraint_column_usage ccu
  ON ccu.constraint_name = tc.constraint_name
 AND ccu.table_schema = tc.table_schema
WHERE tc.table_schema NOT IN ('pg_catalog','information_schema')
ORDER BY tc.table_schema, tc.table_name, tc.constraint_name, kcu.ordinal_position;
```

### 5. Index Discovery
```sql
SELECT schemaname AS table_schema,
       tablename AS table_name,
       indexname AS index_name,
       indexdef AS index_definition
FROM pg_indexes
WHERE schemaname NOT IN ('pg_catalog','information_schema')
ORDER BY schemaname, tablename, indexname;
```

### 6. Sequence Discovery
```sql
SELECT sequence_schema,
       sequence_name,
       data_type,
       start_value,
       minimum_value,
       maximum_value,
       increment,
       cycle_option
FROM information_schema.sequences
WHERE sequence_schema NOT IN ('pg_catalog','information_schema')
ORDER BY sequence_schema, sequence_name;
```

### 7. Function and Procedure DDL Discovery
```sql
SELECT n.nspname AS schema_name,
       p.proname AS routine_name,
       CASE p.prokind WHEN 'p' THEN 'PROCEDURE' ELSE 'FUNCTION' END AS routine_type,
       pg_get_function_identity_arguments(p.oid) AS identity_arguments,
       pg_get_functiondef(p.oid) AS ddl
FROM pg_proc p
JOIN pg_namespace n ON n.oid = p.pronamespace
WHERE n.nspname NOT IN ('pg_catalog','information_schema')
ORDER BY n.nspname, p.proname;
```

### 8. Trigger Discovery
```sql
SELECT event_object_schema AS trigger_schema,
       event_object_table AS table_name,
       trigger_name,
       action_timing,
       event_manipulation,
       action_statement
FROM information_schema.triggers
WHERE trigger_schema NOT IN ('pg_catalog','information_schema')
ORDER BY event_object_schema, event_object_table, trigger_name;
```

### 9. Database Object Inventory
```sql
SELECT n.nspname AS schema_name,
       c.relname AS object_name,
       CASE c.relkind
         WHEN 'r' THEN 'TABLE'
         WHEN 'v' THEN 'VIEW'
         WHEN 'm' THEN 'MATERIALIZED VIEW'
         WHEN 'S' THEN 'SEQUENCE'
         WHEN 'i' THEN 'INDEX'
         WHEN 'f' THEN 'FOREIGN TABLE'
         WHEN 'p' THEN 'PARTITIONED TABLE'
       END AS object_type,
       pg_get_userbyid(c.relowner) AS owner
FROM pg_class c
JOIN pg_namespace n ON n.oid = c.relnamespace
WHERE n.nspname NOT IN ('pg_catalog','information_schema')
  AND c.relkind IN ('r','v','m','S','i','f','p')
ORDER BY n.nspname, object_type, object_name;
```

### 10. Object Comments Discovery
```sql
SELECT n.nspname AS schema_name,
       c.relname AS table_name,
       obj_description(c.oid) AS table_comment
FROM pg_class c
JOIN pg_namespace n ON n.oid = c.relnamespace
WHERE n.nspname NOT IN ('pg_catalog','information_schema')
  AND c.relkind IN ('r','v','m','f','p')
ORDER BY n.nspname, c.relname;
```

## Step 4 – Normalize Metadata Summary

### Normalized Platform-Independent Object Summary
| object_domain | schema_name | object_name | normalized_object_type | source_object_type | owner | comment |
| --- | --- | --- | --- | --- | --- | --- |
| structural | ontology | dim_contract | table | TABLE | ontologyuser1 | |
| structural | ontology | dim_customer | table | TABLE | ontologyuser1 | |
| structural | ontology | dim_date | table | TABLE | ontologyuser1 | |
| structural | ontology | dim_geography | table | TABLE | ontologyuser1 | |
| structural | ontology | dim_partner | table | TABLE | ontologyuser1 | |
| structural | ontology | dim_product | table | TABLE | ontologyuser1 | |
| structural | ontology | dim_sales_rep | table | TABLE | ontologyuser1 | |
| structural | ontology | fact_bookings | table | TABLE | ontologyuser1 | |
| access_path | ontology | dim_contract_pkey | index | INDEX | ontologyuser1 | |
| access_path | ontology | dim_customer_pkey | index | INDEX | ontologyuser1 | |
| access_path | ontology | dim_date_pkey | index | INDEX | ontologyuser1 | |
| access_path | ontology | dim_geography_pkey | index | INDEX | ontologyuser1 | |
| access_path | ontology | dim_partner_pkey | index | INDEX | ontologyuser1 | |
| access_path | ontology | dim_product_pkey | index | INDEX | ontologyuser1 | |
| access_path | ontology | dim_sales_rep_pkey | index | INDEX | ontologyuser1 | |
| access_path | ontology | fact_bookings_pkey | index | INDEX | ontologyuser1 | |

### Normalized Entity Summary
| entity_name | normalized_role | grain_or_purpose | primary_key |
| --- | --- | --- | --- |
| dim_contract | dimension | Contract attributes and coverage descriptors | contract_key |
| dim_customer | dimension | Customer master attributes | customer_key |
| dim_date | dimension | Calendar and fiscal date attributes | date_key |
| dim_geography | dimension | Geographic rollup attributes | geography_key |
| dim_partner | dimension | Partner master attributes | partner_key |
| dim_product | dimension | Product catalog attributes | product_key |
| dim_sales_rep | dimension | Sales representative attributes | sales_rep_key |
| fact_bookings | fact | Booking transaction fact at booking/order line level | booking_id |

### Normalized Relationship Summary
| relationship_name | parent_entity | parent_key | child_entity | child_foreign_key | cardinality | relationship_type |
| --- | --- | --- | --- | --- | --- | --- |
| fk_booking_contract | dim_contract | contract_key | fact_bookings | contract_key | 1-to-many | foreign_key |
| fk_booking_customer | dim_customer | customer_key | fact_bookings | customer_key | 1-to-many | foreign_key |
| fk_booking_date | dim_date | date_key | fact_bookings | date_key | 1-to-many | foreign_key |
| fk_booking_geography | dim_geography | geography_key | fact_bookings | geography_key | 1-to-many | foreign_key |
| fk_booking_partner | dim_partner | partner_key | fact_bookings | partner_key | 1-to-many | foreign_key |
| fk_booking_product | dim_product | product_key | fact_bookings | product_key | 1-to-many | foreign_key |
| fk_booking_sales_rep | dim_sales_rep | sales_rep_key | fact_bookings | sales_rep_key | 1-to-many | foreign_key |

### Normalized Constraint Summary
| constraint_name | schema_name | table_name | constraint_type | column_name | referenced_table | referenced_column |
| --- | --- | --- | --- | --- | --- | --- |
| dim_contract_pkey | ontology | dim_contract | primary_key | contract_key | dim_contract | contract_key |
| dim_customer_pkey | ontology | dim_customer | primary_key | customer_key | dim_customer | customer_key |
| dim_date_pkey | ontology | dim_date | primary_key | date_key | dim_date | date_key |
| dim_geography_pkey | ontology | dim_geography | primary_key | geography_key | dim_geography | geography_key |
| dim_partner_pkey | ontology | dim_partner | primary_key | partner_key | dim_partner | partner_key |
| dim_product_pkey | ontology | dim_product | primary_key | product_key | dim_product | product_key |
| dim_sales_rep_pkey | ontology | dim_sales_rep | primary_key | sales_rep_key | dim_sales_rep | sales_rep_key |
| fact_bookings_pkey | ontology | fact_bookings | primary_key | booking_id | fact_bookings | booking_id |
| fk_booking_contract | ontology | fact_bookings | foreign_key | contract_key | dim_contract | contract_key |
| fk_booking_customer | ontology | fact_bookings | foreign_key | customer_key | dim_customer | customer_key |
| fk_booking_date | ontology | fact_bookings | foreign_key | date_key | dim_date | date_key |
| fk_booking_geography | ontology | fact_bookings | foreign_key | geography_key | dim_geography | geography_key |
| fk_booking_partner | ontology | fact_bookings | foreign_key | partner_key | dim_partner | partner_key |
| fk_booking_product | ontology | fact_bookings | foreign_key | product_key | dim_product | product_key |
| fk_booking_sales_rep | ontology | fact_bookings | foreign_key | sales_rep_key | dim_sales_rep | sales_rep_key |

## Validated Data Dictionary

### Schema Overview
- **Schema Count:** 1 user schema discovered
- **Primary User Schema:** ontology
- **Table Count:** 8
- **View Count:** 0
- **Materialized View Count:** 0
- **Index Count:** 8
- **Sequence Count:** 0
- **Stored Procedure Count:** 0
- **Function Count:** 0
- **Trigger Count:** 0
- **Foreign Key Count:** 7
- **Primary Key Count:** 8

## Structural Schema Metadata

### Table: `ontology.dim_contract`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| contract_key | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| contract_type | 2 | character varying | varchar | YES |  | 40 |  |  | attribute |
| term_months | 3 | integer | int4 | YES |  |  | 32 | 0 | attribute |
| auto_renew_flag | 4 | character | bpchar | YES |  | 1 |  |  | attribute |
| coverage_level | 5 | character varying | varchar | YES |  | 20 |  |  | attribute |

**Keys and Constraints**
- Primary Key: `dim_contract_pkey` on (`contract_key`)

**Indexes**
- `dim_contract_pkey`: `CREATE UNIQUE INDEX dim_contract_pkey ON ontology.dim_contract USING btree (contract_key)`

**DDL Definition**
```sql
CREATE TABLE ontology.dim_contract (
    contract_key integer NOT NULL,
    contract_type varchar(40),
    term_months integer,
    auto_renew_flag char(1),
    coverage_level varchar(20),
    CONSTRAINT dim_contract_pkey PRIMARY KEY (contract_key)
);
```

---

### Table: `ontology.dim_customer`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| customer_key | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| customer_id | 2 | character varying | varchar | NO |  | 20 |  |  | business_identifier |
| customer_name | 3 | character varying | varchar | YES |  | 80 |  |  | descriptive_attribute |
| segment | 4 | character varying | varchar | YES |  | 30 |  |  | classification |
| industry | 5 | character varying | varchar | YES |  | 40 |  |  | classification |
| account_tier | 6 | character varying | varchar | YES |  | 20 |  |  | classification |
| hq_country | 7 | character varying | varchar | YES |  | 40 |  |  | geography_attribute |
| hq_region | 8 | character varying | varchar | YES |  | 20 |  |  | geography_attribute |

**Keys and Constraints**
- Primary Key: `dim_customer_pkey` on (`customer_key`)
- Required Column: `customer_key`
- Required Column: `customer_id`

**Indexes**
- `dim_customer_pkey`: `CREATE UNIQUE INDEX dim_customer_pkey ON ontology.dim_customer USING btree (customer_key)`

**DDL Definition**
```sql
CREATE TABLE ontology.dim_customer (
    customer_key integer NOT NULL,
    customer_id varchar(20) NOT NULL,
    customer_name varchar(80),
    segment varchar(30),
    industry varchar(40),
    account_tier varchar(20),
    hq_country varchar(40),
    hq_region varchar(20),
    CONSTRAINT dim_customer_pkey PRIMARY KEY (customer_key)
);
```

---

### Table: `ontology.dim_date`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| date_key | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| full_date | 2 | date | date | NO |  |  |  |  | natural_key |
| month_name | 3 | character varying | varchar | YES |  | 12 |  |  | calendar_attribute |
| calendar_year | 4 | integer | int4 | YES |  |  | 32 | 0 | calendar_attribute |
| fiscal_year | 5 | character varying | varchar | YES |  | 6 |  |  | fiscal_attribute |
| fiscal_quarter | 6 | character varying | varchar | YES |  | 10 |  |  | fiscal_attribute |
| fiscal_period_seq | 7 | integer | int4 | YES |  |  | 32 | 0 | fiscal_attribute |

**Keys and Constraints**
- Primary Key: `dim_date_pkey` on (`date_key`)
- Required Column: `date_key`
- Required Column: `full_date`

**Indexes**
- `dim_date_pkey`: `CREATE UNIQUE INDEX dim_date_pkey ON ontology.dim_date USING btree (date_key)`

**DDL Definition**
```sql
CREATE TABLE ontology.dim_date (
    date_key integer NOT NULL,
    full_date date NOT NULL,
    month_name varchar(12),
    calendar_year integer,
    fiscal_year varchar(6),
    fiscal_quarter varchar(10),
    fiscal_period_seq integer,
    CONSTRAINT dim_date_pkey PRIMARY KEY (date_key)
);
```

---

### Table: `ontology.dim_geography`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| geography_key | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| region | 2 | character varying | varchar | YES |  | 20 |  |  | geography_attribute |
| theater | 3 | character varying | varchar | YES |  | 30 |  |  | geography_attribute |
| country | 4 | character varying | varchar | YES |  | 40 |  |  | geography_attribute |

**Keys and Constraints**
- Primary Key: `dim_geography_pkey` on (`geography_key`)

**Indexes**
- `dim_geography_pkey`: `CREATE UNIQUE INDEX dim_geography_pkey ON ontology.dim_geography USING btree (geography_key)`

**DDL Definition**
```sql
CREATE TABLE ontology.dim_geography (
    geography_key integer NOT NULL,
    region varchar(20),
    theater varchar(30),
    country varchar(40),
    CONSTRAINT dim_geography_pkey PRIMARY KEY (geography_key)
);
```

---

### Table: `ontology.dim_partner`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| partner_key | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| partner_id | 2 | character varying | varchar | NO |  | 20 |  |  | business_identifier |
| partner_name | 3 | character varying | varchar | YES |  | 60 |  |  | descriptive_attribute |
| partner_type | 4 | character varying | varchar | YES |  | 30 |  |  | classification |
| partner_tier | 5 | character varying | varchar | YES |  | 30 |  |  | classification |
| route_to_market | 6 | character varying | varchar | YES |  | 20 |  |  | classification |

**Keys and Constraints**
- Primary Key: `dim_partner_pkey` on (`partner_key`)
- Required Column: `partner_key`
- Required Column: `partner_id`

**Indexes**
- `dim_partner_pkey`: `CREATE UNIQUE INDEX dim_partner_pkey ON ontology.dim_partner USING btree (partner_key)`

**DDL Definition**
```sql
CREATE TABLE ontology.dim_partner (
    partner_key integer NOT NULL,
    partner_id varchar(20) NOT NULL,
    partner_name varchar(60),
    partner_type varchar(30),
    partner_tier varchar(30),
    route_to_market varchar(20),
    CONSTRAINT dim_partner_pkey PRIMARY KEY (partner_key)
);
```

---

### Table: `ontology.dim_product`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| product_key | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| product_id | 2 | character varying | varchar | NO |  | 30 |  |  | business_identifier |
| product_name | 3 | character varying | varchar | YES |  | 80 |  |  | descriptive_attribute |
| product_family | 4 | character varying | varchar | YES |  | 30 |  |  | classification |
| technology_domain | 5 | character varying | varchar | YES |  | 40 |  |  | classification |
| offer_type | 6 | character varying | varchar | YES |  | 30 |  |  | classification |
| business_entity | 7 | character varying | varchar | YES |  | 30 |  |  | classification |

**Keys and Constraints**
- Primary Key: `dim_product_pkey` on (`product_key`)
- Required Column: `product_key`
- Required Column: `product_id`

**Indexes**
- `dim_product_pkey`: `CREATE UNIQUE INDEX dim_product_pkey ON ontology.dim_product USING btree (product_key)`

**DDL Definition**
```sql
CREATE TABLE ontology.dim_product (
    product_key integer NOT NULL,
    product_id varchar(30) NOT NULL,
    product_name varchar(80),
    product_family varchar(30),
    technology_domain varchar(40),
    offer_type varchar(30),
    business_entity varchar(30),
    CONSTRAINT dim_product_pkey PRIMARY KEY (product_key)
);
```

---

### Table: `ontology.dim_sales_rep`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| sales_rep_key | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| rep_id | 2 | character varying | varchar | NO |  | 20 |  |  | business_identifier |
| rep_name | 3 | character varying | varchar | YES |  | 60 |  |  | descriptive_attribute |
| sales_role | 4 | character varying | varchar | YES |  | 40 |  |  | classification |
| sales_team | 5 | character varying | varchar | YES |  | 40 |  |  | organization_attribute |
| segment_covered | 6 | character varying | varchar | YES |  | 30 |  |  | classification |

**Keys and Constraints**
- Primary Key: `dim_sales_rep_pkey` on (`sales_rep_key`)
- Required Column: `sales_rep_key`
- Required Column: `rep_id`

**Indexes**
- `dim_sales_rep_pkey`: `CREATE UNIQUE INDEX dim_sales_rep_pkey ON ontology.dim_sales_rep USING btree (sales_rep_key)`

**DDL Definition**
```sql
CREATE TABLE ontology.dim_sales_rep (
    sales_rep_key integer NOT NULL,
    rep_id varchar(20) NOT NULL,
    rep_name varchar(60),
    sales_role varchar(40),
    sales_team varchar(40),
    segment_covered varchar(30),
    CONSTRAINT dim_sales_rep_pkey PRIMARY KEY (sales_rep_key)
);
```

---

### Table: `ontology.fact_bookings`
**Object Type:** Table  
**Owner:** ontologyuser1  
**Description:** None available

| column_name | ordinal_position | data_type | native_type | nullable | default | max_length | precision | scale | semantic_role |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| booking_id | 1 | integer | int4 | NO |  |  | 32 | 0 | primary_key |
| order_number | 2 | character varying | varchar | YES |  | 20 |  |  | business_identifier |
| order_line_number | 3 | integer | int4 | YES |  |  | 32 | 0 | transaction_attribute |
| date_key | 4 | integer | int4 | YES |  |  | 32 | 0 | foreign_key |
| customer_key | 5 | integer | int4 | YES |  |  | 32 | 0 | foreign_key |
| product_key | 6 | integer | int4 | YES |  |  | 32 | 0 | foreign_key |
| partner_key | 7 | integer | int4 | YES |  |  | 32 | 0 | foreign_key |
| geography_key | 8 | integer | int4 | YES |  |  | 32 | 0 | foreign_key |
| sales_rep_key | 9 | integer | int4 | YES |  |  | 32 | 0 | foreign_key |
| contract_key | 10 | integer | int4 | YES |  |  | 32 | 0 | foreign_key |
| booking_type | 11 | character varying | varchar | YES |  | 15 |  |  | classification |
| is_renewal | 12 | integer | int4 | YES |  |  | 32 | 0 | indicator |
| quantity | 13 | integer | int4 | YES |  |  | 32 | 0 | measure |
| unit_list_price_usd | 14 | numeric | numeric | YES |  |  | 12 | 2 | measure |
| discount_pct | 15 | numeric | numeric | YES |  |  | 5 | 2 | measure |
| booking_amount_usd | 16 | numeric | numeric | YES |  |  | 14 | 2 | measure |
| acv_usd | 17 | numeric | numeric | YES |  |  | 14 | 2 | measure |
| tcv_usd | 18 | numeric | numeric | YES |  |  | 14 | 2 | measure |

**Keys and Constraints**
- Primary Key: `fact_bookings_pkey` on (`booking_id`)
- Foreign Key: `fk_booking_contract` on (`contract_key`) references `ontology.dim_contract(contract_key)`
- Foreign Key: `fk_booking_customer` on (`customer_key`) references `ontology.dim_customer(customer_key)`
- Foreign Key: `fk_booking_date` on (`date_key`) references `ontology.dim_date(date_key)`
- Foreign Key: `fk_booking_geography` on (`geography_key`) references `ontology.dim_geography(geography_key)`
- Foreign Key: `fk_booking_partner` on (`partner_key`) references `ontology.dim_partner(partner_key)`
- Foreign Key: `fk_booking_product` on (`product_key`) references `ontology.dim_product(product_key)`
- Foreign Key: `fk_booking_sales_rep` on (`sales_rep_key`) references `ontology.dim_sales_rep(sales_rep_key)`

**Indexes**
- `fact_bookings_pkey`: `CREATE UNIQUE INDEX fact_bookings_pkey ON ontology.fact_bookings USING btree (booking_id)`

**DDL Definition**
```sql
CREATE TABLE ontology.fact_bookings (
    booking_id integer NOT NULL,
    order_number varchar(20),
    order_line_number integer,
    date_key integer,
    customer_key integer,
    product_key integer,
    partner_key integer,
    geography_key integer,
    sales_rep_key integer,
    contract_key integer,
    booking_type varchar(15),
    is_renewal integer,
    quantity integer,
    unit_list_price_usd numeric(12,2),
    discount_pct numeric(5,2),
    booking_amount_usd numeric(14,2),
    acv_usd numeric(14,2),
    tcv_usd numeric(14,2),
    CONSTRAINT fact_bookings_pkey PRIMARY KEY (booking_id),
    CONSTRAINT fk_booking_contract FOREIGN KEY (contract_key) REFERENCES ontology.dim_contract(contract_key),
    CONSTRAINT fk_booking_customer FOREIGN KEY (customer_key) REFERENCES ontology.dim_customer(customer_key),
    CONSTRAINT fk_booking_date FOREIGN KEY (date_key) REFERENCES ontology.dim_date(date_key),
    CONSTRAINT fk_booking_geography FOREIGN KEY (geography_key) REFERENCES ontology.dim_geography(geography_key),
    CONSTRAINT fk_booking_partner FOREIGN KEY (partner_key) REFERENCES ontology.dim_partner(partner_key),
    CONSTRAINT fk_booking_product FOREIGN KEY (product_key) REFERENCES ontology.dim_product(product_key),
    CONSTRAINT fk_booking_sales_rep FOREIGN KEY (sales_rep_key) REFERENCES ontology.dim_sales_rep(sales_rep_key)
);
```

## Database Object Metadata

### Tables
- ontology.dim_contract
- ontology.dim_customer
- ontology.dim_date
- ontology.dim_geography
- ontology.dim_partner
- ontology.dim_product
- ontology.dim_sales_rep
- ontology.fact_bookings

### Views
- None discovered

### Indexes
- ontology.dim_contract_pkey
- ontology.dim_customer_pkey
- ontology.dim_date_pkey
- ontology.dim_geography_pkey
- ontology.dim_partner_pkey
- ontology.dim_product_pkey
- ontology.dim_sales_rep_pkey
- ontology.fact_bookings_pkey

### Constraints
- Primary Keys: 8
- Foreign Keys: 7
- System-generated NOT NULL enforcement checks observed in metadata but excluded from business constraint normalization

### Sequences
- None discovered

### Stored Procedures
- None discovered

### Functions
- None discovered

### Triggers
- None discovered

## Relationships
| parent_table | parent_column | child_table | child_column | relationship_name |
| --- | --- | --- | --- | --- |
| ontology.dim_contract | contract_key | ontology.fact_bookings | contract_key | fk_booking_contract |
| ontology.dim_customer | customer_key | ontology.fact_bookings | customer_key | fk_booking_customer |
| ontology.dim_date | date_key | ontology.fact_bookings | date_key | fk_booking_date |
| ontology.dim_geography | geography_key | ontology.fact_bookings | geography_key | fk_booking_geography |
| ontology.dim_partner | partner_key | ontology.fact_bookings | partner_key | fk_booking_partner |
| ontology.dim_product | product_key | ontology.fact_bookings | product_key | fk_booking_product |
| ontology.dim_sales_rep | sales_rep_key | ontology.fact_bookings | sales_rep_key | fk_booking_sales_rep |

## Keys

### Primary Keys
| table_name | primary_key_column |
| --- | --- |
| dim_contract | contract_key |
| dim_customer | customer_key |
| dim_date | date_key |
| dim_geography | geography_key |
| dim_partner | partner_key |
| dim_product | product_key |
| dim_sales_rep | sales_rep_key |
| fact_bookings | booking_id |

### Foreign Keys
| table_name | foreign_key_column | references_table | references_column |
| --- | --- | --- | --- |
| fact_bookings | contract_key | dim_contract | contract_key |
| fact_bookings | customer_key | dim_customer | customer_key |
| fact_bookings | date_key | dim_date | date_key |
| fact_bookings | geography_key | dim_geography | geography_key |
| fact_bookings | partner_key | dim_partner | partner_key |
| fact_bookings | product_key | dim_product | product_key |
| fact_bookings | sales_rep_key | dim_sales_rep | sales_rep_key |

## Indexes
| schema_name | table_name | index_name | index_definition |
| --- | --- | --- | --- |
| ontology | dim_contract | dim_contract_pkey | CREATE UNIQUE INDEX dim_contract_pkey ON ontology.dim_contract USING btree (contract_key) |
| ontology | dim_customer | dim_customer_pkey | CREATE UNIQUE INDEX dim_customer_pkey ON ontology.dim_customer USING btree (customer_key) |
| ontology | dim_date | dim_date_pkey | CREATE UNIQUE INDEX dim_date_pkey ON ontology.dim_date USING btree (date_key) |
| ontology | dim_geography | dim_geography_pkey | CREATE UNIQUE INDEX dim_geography_pkey ON ontology.dim_geography USING btree (geography_key) |
| ontology | dim_partner | dim_partner_pkey | CREATE UNIQUE INDEX dim_partner_pkey ON ontology.dim_partner USING btree (partner_key) |
| ontology | dim_product | dim_product_pkey | CREATE UNIQUE INDEX dim_product_pkey ON ontology.dim_product USING btree (product_key) |
| ontology | dim_sales_rep | dim_sales_rep_pkey | CREATE UNIQUE INDEX dim_sales_rep_pkey ON ontology.dim_sales_rep USING btree (sales_rep_key) |
| ontology | fact_bookings | fact_bookings_pkey | CREATE UNIQUE INDEX fact_bookings_pkey ON ontology.fact_bookings USING btree (booking_id) |

## Step 5 – Extract DDL Information

### DDL Coverage Status
| object_type | discovered_count | ddl_available | notes |
| --- | --- | --- | --- |
| tables | 8 | yes | Reconstructed from catalog metadata and constraints |
| views | 0 | no | No views discovered |
| indexes | 8 | yes | Retrieved directly from `pg_indexes.indexdef` |
| constraints | 15 | yes | PK and FK definitions represented in reconstructed table DDL |
| sequences | 0 | no | No sequences discovered |
| stored procedures | 0 | no | No procedures discovered |
| functions | 0 | no | No functions discovered |
| triggers | 0 | no | No triggers discovered |

### Index DDL Definitions
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

## Platform-Independent Normalized Metadata for Downstream Use

```yaml
platform: postgresql
source_database: ontology
source_schema: ontology
normalized_model:
  subject_area: bookings_analytics
  entities:
    - name: dim_contract
      type: dimension
      primary_key: contract_key
      attributes:
        - contract_key
        - contract_type
        - term_months
        - auto_renew_flag
        - coverage_level
    - name: dim_customer
      type: dimension
      primary_key: customer_key
      business_keys:
        - customer_id
      attributes:
        - customer_name
        - segment
        - industry
        - account_tier
        - hq_country
        - hq_region
    - name: dim_date
      type: dimension
      primary_key: date_key
      natural_keys:
        - full_date
      attributes:
        - month_name
        - calendar_year
        - fiscal_year
        - fiscal_quarter
        - fiscal_period_seq
    - name: dim_geography
      type: dimension
      primary_key: geography_key
      attributes:
        - region
        - theater
        - country
    - name: dim_partner
      type: dimension
      primary_key: partner_key
      business_keys:
        - partner_id
      attributes:
        - partner_name
        - partner_type
        - partner_tier
        - route_to_market
    - name: dim_product
      type: dimension
      primary_key: product_key
      business_keys:
        - product_id
      attributes:
        - product_name
        - product_family
        - technology_domain
        - offer_type
        - business_entity
    - name: dim_sales_rep
      type: dimension
      primary_key: sales_rep_key
      business_keys:
        - rep_id
      attributes:
        - rep_name
        - sales_role
        - sales_team
        - segment_covered
    - name: fact_bookings
      type: fact
      primary_key: booking_id
      foreign_keys:
        - date_key
        - customer_key
        - product_key
        - partner_key
        - geography_key
        - sales_rep_key
        - contract_key
      measures:
        - quantity
        - unit_list_price_usd
        - discount_pct
        - booking_amount_usd
        - acv_usd
        - tcv_usd
      descriptors:
        - order_number
        - order_line_number
        - booking_type
        - is_renewal
  relationships:
    - name: fk_booking_contract
      from_entity: fact_bookings
      from_attribute: contract_key
      to_entity: dim_contract
      to_attribute: contract_key
    - name: fk_booking_customer
      from_entity: fact_bookings
      from_attribute: customer_key
      to_entity: dim_customer
      to_attribute: customer_key
    - name: fk_booking_date
      from_entity: fact_bookings
      from_attribute: date_key
      to_entity: dim_date
      to_attribute: date_key
    - name: fk_booking_geography
      from_entity: fact_bookings
      from_attribute: geography_key
      to_entity: dim_geography
      to_attribute: geography_key
    - name: fk_booking_partner
      from_entity: fact_bookings
      from_attribute: partner_key
      to_entity: dim_partner
      to_attribute: partner_key
    - name: fk_booking_product
      from_entity: fact_bookings
      from_attribute: product_key
      to_entity: dim_product
      to_attribute: product_key
    - name: fk_booking_sales_rep
      from_entity: fact_bookings
      from_attribute: sales_rep_key
      to_entity: dim_sales_rep
      to_attribute: sales_rep_key
```

## Validation Notes
- Metadata was successfully extracted from PostgreSQL system catalogs and information schema views.
- All 8 discovered user tables were documented.
- All discovered primary keys and foreign keys were captured.
- Index metadata was captured for every discovered table.
- No views, sequences, routines, or triggers were present in the discovered schema.
- Table DDL was reconstructed from validated structural metadata because direct `pg_get_tabledef` support is not available in standard PostgreSQL catalogs.
- The resulting data dictionary is suitable for enterprise documentation, metadata governance, semantic modeling, ontology generation, cataloging, and AI-driven schema discovery.
