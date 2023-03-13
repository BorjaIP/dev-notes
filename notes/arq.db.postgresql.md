---
id: rqncsuqjf53tw5ea98sqsrq
title: PostgreSQL
desc: ''
updated: 1678700253832
created: 1655362493969
---

```bash
# access DB
psql -h localhost -U admin -W 
psql -d postgres -U webadmin -W
# AWS
psql -U user -h hostname.rds.amazonaws.com -p 5432 database

# list all DB
\l
\c database;
\dn
# list tables
\dt 

# exit
\q
 
# delete table in DB
DELETE FROM tablename;

# ACCESS DB
REVOKE CONNECT ON DATABASE nova FROM PUBLIC;
GRANT  CONNECT ON DATABASE nova  TO user;

# ACCESS SCHEMA
REVOKE ALL     ON SCHEMA public FROM PUBLIC;
GRANT  USAGE   ON SCHEMA public  TO user;

# ACCESS TABLES
REVOKE ALL ON ALL TABLES IN SCHEMA public FROM PUBLIC ;
GRANT SELECT   ON ALL TABLES IN SCHEMA public TO read_only ;
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO read_write ;
GRANT ALL ON ALL TABLES IN SCHEMA public TO admin ;

# create 
CREATE USER user WITH PASSWORD 'pass';
CREATE DATABASE database;
GRANT ALL PRIVILEGES ON DATABASE database TO user;
GRANT ALL PRIVILEGES ON SCHEMA database TO user;

# Delete all conections
SELECT
	pg_terminate_backend(pg_stat_activity.pid)
FROM
	pg_stat_activity
WHERE
	pg_stat_activity.datname = 'database_name'
	AND pid <> pg_backend_pid();

# Creats sample data
CREATE TABLE products (
	product_name char(50),
	price int
)

INSERT INTO products (product_name, price)
VALUES
('Desktop Computer',800),
('Laptop',1200),
('Tablet',200),
('Monitor',350),
('Printer',150)
SELECT * FROM products
```

## Security

[Generate TLS](https://www.crunchydata.com/blog/ssl-certificate-authentication-postgresql-docker-containers)