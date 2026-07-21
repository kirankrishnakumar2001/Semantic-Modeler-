# Metadata Summary

## Source System Identification
- **Database Platform:** PostgreSQL
- **Database Name:** ontology
- **Active Schema:** ontology
- **Server Version:** PostgreSQL 16.14 on x86_64-pc-linux-gnu, compiled by gcc (GCC) 13.2.0, 64-bit

## Step 3 – Database-Specific Metadata SQL
The following PostgreSQL-specific SQL statements were used to discover metadata from system catalogs and information schema.

### 1. Platform Detection
```sql
SELECT current_database() AS database_name, current_schema() AS current_schema, version() AS version;
```

### 2. Table Discovery
```sql
SELECT table_schema, table_name, table_type
FROM information_schema.tables
WHERE table_schema NOT IN ('pg_catalog','information_schema')
ORDER BY table_schema, table_name;
```

### 3. Column Discovery
```sql
SELECT table_schema, table_name, column_name, ordinal_position, data_type, udt_name, is_nullable,
       column_default, character_maximum_length, numeric_precision, numeric_scale
FROM information_schema.columns
WHERE table_schema NOT IN ('pg_catalog','information_schema')
ORDER BY table_schema, table_name, ordinal_position;
```

### 4. Constraint and Relationship Discovery
```sql
SELECT tc.table_schema, tc.table_name, tc.constraint_name, tc.constraint_type, kcu.column_name,
       ccu.table_schema AS foreign_table_schema, ccu.table_name AS foreign_table_name,
       ccu.column_name AS foreign_column_name
FROM information_schema.table_constraints tc
LEFT JOIN information_schema.key_column_usage kcu
  ON tc.constraint_name = kcu.constraint_name
 AND tc.table_schema = kcu.table_schema
 AND tc.table_name = kcu.table_name
LEFT JOIN information_schema.constraint_column_usage ccu
  ON tc.constraint_name = ccu.constraint_name
 AND tc.table_schema = ccu.table_schema
WHERE tc.table_schema NOT IN ('pg_catalog','information_schema')
ORDER BY tc.table_schema, tc.table_name, tc.constraint_name, kcu.ordinal_position;
```

### 5. Index Discovery
```sql
SELECT schemaname AS table_schema, tablename AS table_name, indexname, indexdef
FROM pg_indexes
WHERE schemaname NOT IN ('pg_catalog','information_schema')
ORDER BY schemaname, tablename, indexname;
```

### 6. Sequence Discovery
```sql
SELECT sequence_schema, sequence_name, data_type, start_value, minimum_value,
       maximum_value, increment, cycle_option
FROM information_schema.sequences
WHERE sequence_schema NOT IN ('pg_catalog','information_schema')
ORDER BY sequence_schema, sequence_name;
```

### 7. Function and Procedure DDL Discovery
```sql
SELECT n.nspname AS routine_schema,
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
SELECT event_object_schema AS trigger_schema, event_object_table AS table_name, trigger_name,
       action_timing, event_manipulation, action_statement
FROM information_schema.triggers
WHERE trigger_schema NOT IN ('pg_catalog','information_schema')
ORDER BY event_object_schema, event_object_table, trigger_name;
```

### 9. View Discovery
```sql
SELECT schemaname AS object_schema, viewname AS object_name, definition
FROM pg_views
WHERE schemaname NOT IN ('pg_catalog','information_schema')
ORDER BY schemaname, viewname;
```

### 10. View DDL Discovery
```sql
SELECT n.nspname AS schema_name, c.relname AS object_name, c.relkind,
       pg_get_viewdef(c.oid, true) AS view_ddl_or_definition
FROM pg_class c
JOIN pg_namespace n ON n.oid = c.relnamespace
WHERE c.relkind IN ('v','m')
  AND n.nspname NOT IN ('pg_catalog','information_schema')
ORDER BY n.nspname, c.relname;
```

### 11. Constraint DDL Discovery
```sql
SELECT n.nspname AS schema_name,
       c.relname AS table_name,
       pg_get_constraintdef(con.oid, true) AS constraint_definition,
       con.conname AS constraint_name,
       CASE con.contype
         WHEN 'p' THEN 'PRIMARY KEY'
         WHEN 'f' THEN 'FOREIGN KEY'
         WHEN 'u' THEN 'UNIQUE'
         WHEN 'c' THEN 'CHECK'
         ELSE con.contype::text
       END AS constraint_type
FROM pg_constraint con
JOIN pg_class c ON c.oid = con.conrelid
JOIN pg_namespace n ON n.oid = c.relnamespace
WHERE n.nspname NOT IN ('pg_catalog','information_schema')
ORDER BY n.nspname, c.relname, con.conname;
```

### 12. Trigger DDL Discovery
```sql
SELECT n.nspname AS schema_name,
       c.relname AS table_name,
       pg_get_triggerdef(t.oid, true) AS trigger_ddl,
       t.tgname AS trigger_name
FROM pg_trigger t
JOIN pg_class c ON c.oid = t.tgrelid
JOIN pg_namespace n ON n.oid = c.relnamespace
WHERE NOT t.tgisinternal
  AND n.nspname NOT IN ('pg_catalog','information_schema')
ORDER BY n.nspname, c.relname, t.tgname;
```

## Step 4 – Normalize Metadata Summary
The extracted PostgreSQL metadata has been normalized into a platform-independent structure for enterprise metadata management.

### Normalized Object Inventory
| object_category | schema_name | object_name | object_type | status |
| --- | --- | --- | --- | --- |
| table | ontology | dim_contract | dimension | discovered |
| table | ontology | dim_customer | dimension | discovered |
| table | ontology | dim_date | dimension | discovered |
| table | ontology | dim_geography | dimension | discovered |
| table | ontology | dim_partner | dimension | discovered |
| table | ontology | dim_product | dimension | discovered |
| table | ontology | dim_sales_rep | dimension | discovered |
| table | ontology | fact_bookings | fact | discovered |
| view | ontology | none | none | not present |
| sequence | ontology | none | none | not present |
| procedure | ontology | none | none | not present |
| function | ontology | none | none | not present |
| trigger | ontology | none | none | not present |

### Normalized Structural Metadata
| schema_name | table_name | column_name | ordinal_position | logical_data_type | physical_data_type | nullable | default_value | max_length | numeric_precision | numeric_scale |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ontology | dim_contract | contract_key | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | dim_contract | contract_type | 2 | string | varchar | YES |  | 40 |  |  |
| ontology | dim_contract | term_months | 3 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | dim_contract | auto_renew_flag | 4 | string | bpchar | YES |  | 1 |  |  |
| ontology | dim_contract | coverage_level | 5 | string | varchar | YES |  | 20 |  |  |
| ontology | dim_customer | customer_key | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | dim_customer | customer_id | 2 | string | varchar | NO |  | 20 |  |  |
| ontology | dim_customer | customer_name | 3 | string | varchar | YES |  | 80 |  |  |
| ontology | dim_customer | segment | 4 | string | varchar | YES |  | 30 |  |  |
| ontology | dim_customer | industry | 5 | string | varchar | YES |  | 40 |  |  |
| ontology | dim_customer | account_tier | 6 | string | varchar | YES |  | 20 |  |  |
| ontology | dim_customer | hq_country | 7 | string | varchar | YES |  | 40 |  |  |
| ontology | dim_customer | hq_region | 8 | string | varchar | YES |  | 20 |  |  |
| ontology | dim_date | date_key | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | dim_date | full_date | 2 | date | date | NO |  |  |  |  |
| ontology | dim_date | month_name | 3 | string | varchar | YES |  | 12 |  |  |
| ontology | dim_date | calendar_year | 4 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | dim_date | fiscal_year | 5 | string | varchar | YES |  | 6 |  |  |
| ontology | dim_date | fiscal_quarter | 6 | string | varchar | YES |  | 10 |  |  |
| ontology | dim_date | fiscal_period_seq | 7 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | dim_geography | geography_key | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | dim_geography | region | 2 | string | varchar | YES |  | 20 |  |  |
| ontology | dim_geography | theater | 3 | string | varchar | YES |  | 30 |  |  |
| ontology | dim_geography | country | 4 | string | varchar | YES |  | 40 |  |  |
| ontology | dim_partner | partner_key | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | dim_partner | partner_id | 2 | string | varchar | NO |  | 20 |  |  |
| ontology | dim_partner | partner_name | 3 | string | varchar | YES |  | 60 |  |  |
| ontology | dim_partner | partner_type | 4 | string | varchar | YES |  | 30 |  |  |
| ontology | dim_partner | partner_tier | 5 | string | varchar | YES |  | 30 |  |  |
| ontology | dim_partner | route_to_market | 6 | string | varchar | YES |  | 20 |  |  |
| ontology | dim_product | product_key | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | dim_product | product_id | 2 | string | varchar | NO |  | 30 |  |  |
| ontology | dim_product | product_name | 3 | string | varchar | YES |  | 80 |  |  |
| ontology | dim_product | product_family | 4 | string | varchar | YES |  | 30 |  |  |
| ontology | dim_product | technology_domain | 5 | string | varchar | YES |  | 40 |  |  |
| ontology | dim_product | offer_type | 6 | string | varchar | YES |  | 30 |  |  |
| ontology | dim_product | business_entity | 7 | string | varchar | YES |  | 30 |  |  |
| ontology | dim_sales_rep | sales_rep_key | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | dim_sales_rep | rep_id | 2 | string | varchar | NO |  | 20 |  |  |
| ontology | dim_sales_rep | rep_name | 3 | string | varchar | YES |  | 60 |  |  |
| ontology | dim_sales_rep | sales_role | 4 | string | varchar | YES |  | 40 |  |  |
| ontology | dim_sales_rep | sales_team | 5 | string | varchar | YES |  | 40 |  |  |
| ontology | dim_sales_rep | segment_covered | 6 | string | varchar | YES |  | 30 |  |  |
| ontology | fact_bookings | booking_id | 1 | integer | int4 | NO |  |  | 32 | 0 |
| ontology | fact_bookings | order_number | 2 | string | varchar | YES |  | 20 |  |  |
| ontology | fact_bookings | order_line_number | 3 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | date_key | 4 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | customer_key | 5 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | product_key | 6 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | partner_key | 7 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | geography_key | 8 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | sales_rep_key | 9 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | contract_key | 10 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | booking_type | 11 | string | varchar | YES |  | 15 |  |  |
| ontology | fact_bookings | is_renewal | 12 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | quantity | 13 | integer | int4 | YES |  |  | 32 | 0 |
| ontology | fact_bookings | unit_list_price_usd | 14 | decimal | numeric | YES |  |  | 12 | 2 |
| ontology | fact_bookings | discount_pct | 15 | decimal | numeric | YES |  |  | 5 | 2 |
| ontology | fact_bookings | booking_amount_usd | 16 | decimal | numeric | YES |  |  | 14 | 2 |
| ontology | fact_bookings | acv_usd | 17 | decimal | numeric | YES |  |  | 14 | 2 |
| ontology | fact_bookings | tcv_usd | 18 | decimal | numeric | YES |  |  | 14 | 2 |

## Data Dictionary

### Table: ontology.dim_contract
**Object Type:** Table  
**Business Role:** Dimension

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| contract_key | integer | NO | Primary Key | Surrogate key for contract dimension |
| contract_type | varchar(40) | YES | Attribute | Contract classification |
| term_months | integer | YES | Attribute | Contract duration in months |
| auto_renew_flag | char(1) | YES | Attribute | Indicates whether contract auto-renews |
| coverage_level | varchar(20) | YES | Attribute | Contract coverage level |

### Table: ontology.dim_customer
**Object Type:** Table  
**Business Role:** Dimension

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| customer_key | integer | NO | Primary Key | Surrogate key for customer dimension |
| customer_id | varchar(20) | NO | Business Identifier | Source customer identifier |
| customer_name | varchar(80) | YES | Attribute | Customer name |
| segment | varchar(30) | YES | Attribute | Customer segment |
| industry | varchar(40) | YES | Attribute | Industry classification |
| account_tier | varchar(20) | YES | Attribute | Account tier |
| hq_country | varchar(40) | YES | Attribute | Headquarters country |
| hq_region | varchar(20) | YES | Attribute | Headquarters region |

### Table: ontology.dim_date
**Object Type:** Table  
**Business Role:** Dimension

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| date_key | integer | NO | Primary Key | Surrogate date key |
| full_date | date | NO | Natural Date | Calendar date |
| month_name | varchar(12) | YES | Attribute | Month name |
| calendar_year | integer | YES | Attribute | Calendar year |
| fiscal_year | varchar(6) | YES | Attribute | Fiscal year label |
| fiscal_quarter | varchar(10) | YES | Attribute | Fiscal quarter label |
| fiscal_period_seq | integer | YES | Attribute | Fiscal period sequence |

### Table: ontology.dim_geography
**Object Type:** Table  
**Business Role:** Dimension

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| geography_key | integer | NO | Primary Key | Surrogate key for geography dimension |
| region | varchar(20) | YES | Attribute | Sales region |
| theater | varchar(30) | YES | Attribute | Theater grouping |
| country | varchar(40) | YES | Attribute | Country name |

### Table: ontology.dim_partner
**Object Type:** Table  
**Business Role:** Dimension

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| partner_key | integer | NO | Primary Key | Surrogate key for partner dimension |
| partner_id | varchar(20) | NO | Business Identifier | Source partner identifier |
| partner_name | varchar(60) | YES | Attribute | Partner name |
| partner_type | varchar(30) | YES | Attribute | Partner type |
| partner_tier | varchar(30) | YES | Attribute | Partner tier |
| route_to_market | varchar(20) | YES | Attribute | Route to market |

### Table: ontology.dim_product
**Object Type:** Table  
**Business Role:** Dimension

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| product_key | integer | NO | Primary Key | Surrogate key for product dimension |
| product_id | varchar(30) | NO | Business Identifier | Source product identifier |
| product_name | varchar(80) | YES | Attribute | Product name |
| product_family | varchar(30) | YES | Attribute | Product family |
| technology_domain | varchar(40) | YES | Attribute | Technology domain |
| offer_type | varchar(30) | YES | Attribute | Offer type |
| business_entity | varchar(30) | YES | Attribute | Business entity |

### Table: ontology.dim_sales_rep
**Object Type:** Table  
**Business Role:** Dimension

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| sales_rep_key | integer | NO | Primary Key | Surrogate key for sales representative dimension |
| rep_id | varchar(20) | NO | Business Identifier | Source representative identifier |
| rep_name | varchar(60) | YES | Attribute | Representative name |
| sales_role | varchar(40) | YES | Attribute | Sales role |
| sales_team | varchar(40) | YES | Attribute | Sales team |
| segment_covered | varchar(30) | YES | Attribute | Segment coverage |

### Table: ontology.fact_bookings
**Object Type:** Table  
**Business Role:** Fact

| column_name | data_type | nullable | key_role | description |
| --- | --- | --- | --- | --- |
| booking_id | integer | NO | Primary Key | Unique booking row identifier |
| order_number | varchar(20) | YES | Degenerate Dimension | Sales order number |
| order_line_number | integer | YES | Degenerate Dimension | Order line number |
| date_key | integer | YES | Foreign Key | References dim_date |
| customer_key | integer | YES | Foreign Key | References dim_customer |
| product_key | integer | YES | Foreign Key | References dim_product |
| partner_key | integer | YES | Foreign Key | References dim_partner |
| geography_key | integer | YES | Foreign Key | References dim_geography |
| sales_rep_key | integer | YES | Foreign Key | References dim_sales_rep |
| contract_key | integer | YES | Foreign Key | References dim_contract |
| booking_type | varchar(15) | YES | Attribute | Booking type |
| is_renewal | integer | YES | Indicator | Renewal indicator |
| quantity | integer | YES | Measure | Booked quantity |
| unit_list_price_usd | numeric(12,2) | YES | Measure | Unit list price in USD |
| discount_pct | numeric(5,2) | YES | Measure | Discount percentage |
| booking_amount_usd | numeric(14,2) | YES | Measure | Booking amount in USD |
| acv_usd | numeric(14,2) | YES | Measure | Annual contract value in USD |
| tcv_usd | numeric(14,2) | YES | Measure | Total contract value in USD |

## Relationships
| child_schema | child_table | child_column | relationship_type | parent_schema | parent_table | parent_column |
| --- | --- | --- | --- | --- | --- | --- |
| ontology | fact_bookings | contract_key | many-to-one | ontology | dim_contract | contract_key |
| ontology | fact_bookings | customer_key | many-to-one | ontology | dim_customer | customer_key |
| ontology | fact_bookings | date_key | many-to-one | ontology | dim_date | date_key |
| ontology | fact_bookings | geography_key | many-to-one | ontology | dim_geography | geography_key |
| ontology | fact_bookings | partner_key | many-to-one | ontology | dim_partner | partner_key |
| ontology | fact_bookings | product_key | many-to-one | ontology | dim_product | product_key |
| ontology | fact_bookings | sales_rep_key | many-to-one | ontology | dim_sales_rep | sales_rep_key |

## Keys
| schema_name | table_name | key_name | key_type | column_name |
| --- | --- | --- | --- | --- |
| ontology | dim_contract | dim_contract_pkey | PRIMARY KEY | contract_key |
| ontology | dim_customer | dim_customer_pkey | PRIMARY KEY | customer_key |
| ontology | dim_date | dim_date_pkey | PRIMARY KEY | date_key |
| ontology | dim_geography | dim_geography_pkey | PRIMARY KEY | geography_key |
| ontology | dim_partner | dim_partner_pkey | PRIMARY KEY | partner_key |
| ontology | dim_product | dim_product_pkey | PRIMARY KEY | product_key |
| ontology | dim_sales_rep | dim_sales_rep_pkey | PRIMARY KEY | sales_rep_key |
| ontology | fact_bookings | fact_bookings_pkey | PRIMARY KEY | booking_id |
| ontology | fact_bookings | fk_booking_contract | FOREIGN KEY | contract_key |
| ontology | fact_bookings | fk_booking_customer | FOREIGN KEY | customer_key |
| ontology | fact_bookings | fk_booking_date | FOREIGN KEY | date_key |
| ontology | fact_bookings | fk_booking_geography | FOREIGN KEY | geography_key |
| ontology | fact_bookings | fk_booking_partner | FOREIGN KEY | partner_key |
| ontology | fact_bookings | fk_booking_product | FOREIGN KEY | product_key |
| ontology | fact_bookings | fk_booking_sales_rep | FOREIGN KEY | sales_rep_key |

## Constraints
| schema_name | table_name | constraint_name | constraint_type | constraint_definition |
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

## Step 5 – DDL Information

### Table and Index DDL
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
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_contract FOREIGN KEY (contract_key) REFERENCES ontology.dim_contract(contract_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_customer FOREIGN KEY (customer_key) REFERENCES ontology.dim_customer(customer_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_date FOREIGN KEY (date_key) REFERENCES ontology.dim_date(date_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_geography FOREIGN KEY (geography_key) REFERENCES ontology.dim_geography(geography_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_partner FOREIGN KEY (partner_key) REFERENCES ontology.dim_partner(partner_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_product FOREIGN KEY (product_key) REFERENCES ontology.dim_product(product_key);
ALTER TABLE ontology.fact_bookings ADD CONSTRAINT fk_booking_sales_rep FOREIGN KEY (sales_rep_key) REFERENCES ontology.dim_sales_rep(sales_rep_key);
```

### Views
No user-defined views were discovered.

### Sequences
No user-defined sequences were discovered.

### Stored Procedures
No user-defined stored procedures were discovered.

### Functions
No user-defined functions were discovered.

### Triggers
No user-defined triggers were discovered.

## Validation Summary
- Structural schema metadata extracted successfully.
- Database object metadata extracted successfully.
- Relationships identified successfully.
- Keys and constraints extracted successfully.
- Index metadata extracted successfully.
- DDL definitions retrieved where available from PostgreSQL metadata catalogs.
- Metadata normalized into a platform-independent structure.

## Suitability
This output is suitable for:
- Enterprise documentation
- Metadata governance
- Data cataloging
- Semantic model generation
- Ontology generation
- AI-driven metadata discovery
