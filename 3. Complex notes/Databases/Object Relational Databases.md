It is a enhancement of classical relational databases - adds support for object types (predefined or user defined).

Combines advantages of RDBMS:
- powerful OLTP processing
- availability
- access rights
- administration tools
- standardized languages
- concurrency
- integrity

OODBMS:
- complex objects processing
- recursive structures
- abstract data types

In PostgreSQL:
```sql
CREATE TYPE address AS (
	street VARCHAR(100),
	city VARCHAR(50),
	zip_code VARCHAR(10)
);
CREATE TABLE person (
	id SERIAL PRIMARY KEY,
	name VARCHAR(100), address address );
```
