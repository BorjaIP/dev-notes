---
id: rqncsuqjf53tw5ea98sqsrq
title: PostgreSQL
desc: ''
updated: 1655549265860
created: 1655362493969
---

```bash
# entrar BBDD
psql -h localhost -U admin -W 
psql -d postgres -U webadmin -W

# lista todas las bases de datos
\l
\c database;
\dn
# list tables
\dt 

# Borrar una Tabla de una BBDD
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

# crear 
CREATE USER user WITH PASSWORD 'pass';
CREATE DATABASE database;
GRANT ALL PRIVILEGES ON DATABASE database TO user;
GRANT ALL PRIVILEGES ON SCHEMA database TO user;

# Borrar las conexiones que tiene una Base de datos
SELECT
	pg_terminate_backend(pg_stat_activity.pid)
FROM
	pg_stat_activity
WHERE
	pg_stat_activity.datname = 'database_name'
	AND pid <> pg_backend_pid();
```

## Security

[Generate TLS](https://www.crunchydata.com/blog/ssl-certificate-authentication-postgresql-docker-containers)