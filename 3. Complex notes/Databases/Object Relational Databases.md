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

# Reference to an object (REF)
It is a pointer or a link to a row object in the database. REF can be used to obtain, examine and update the object. REFs are strongly typed - we know what type of data it references. It is a direct link to a row.

# User types in a table vs object table
## Relational table with user types
This is the straight-forward way of using custom user defined types.
```sql
CREATE TYPE Address AS (
    street VARCHAR(100),
    city VARCHAR(50),
    zip_code VARCHAR(10)
);


CREATE TABLE Person (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    address Address  -- using the UDT
);
```

These are normal tables and some of their columns use custom object-oriented types.

## Object table
Tables that directly store instances of user-defined types. They are more closely aligned with OOP.
```sql
CREATE TYPE PersonType AS OBJECT (
    id INT,
    name VARCHAR(100),
    address Address
);

CREATE TABLE PersonTable OF PersonType (
    PRIMARY KEY (id)
);
```
They should store objects that represent one complete thing.
## PostgreSQL
### User data types:
```sql
CREATE TYPE address AS (
	street VARCHAR(100),
	city VARCHAR(50),
	zip_code VARCHAR(10)
);
CREATE TABLE person (
	id SERIAL PRIMARY KEY,
	name VARCHAR(100),
	address address
);
```

### Table inheritance
```sql
CREATE TABLE vehicle (
    vehicle_id SERIAL PRIMARY KEY,
    brand VARCHAR(100),
    model VARCHAR(100)
);
CREATE TABLE car (
    car_specific_feature VARCHAR(100)
) INHERITS (vehicle);
```

### Array types
```sql
CREATE TABLE tech_company (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    product_names VARCHAR(100)[]
);

INSERT INTO tech_company (name, product_names)
VALUES ('TechCorp', ARRAY['Gadget1', 'Gadget2', 'Gadget3']);
```