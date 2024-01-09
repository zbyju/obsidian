# Relational
Classical database model with the deepest history and most versatility.

# Document
Data stored as documents - JSON, BSON, XML or similar formats. Each documents is a self-contained unit and can have a different structure. This allows for a more natural and intuitive data representation.

Databases: MongoDB, DynamoDB, Couchbase

## Schema-less structure
They are schema-less so you can insert any document under the same collection together.

## Other features
They still support indexes, querying, aggregations. These databases are usually still very versatile.

Usually problem with JOIN operations, need for denormalization.

## Comparison
##### Pros:
- Schema flexibility
	- Adapts well to changes
- Scalability
	- Often built for easy horizontal scaling
- Developer-friendly
	- Data in format the devs are used to and can easily integrate with the rest of the application
- Speed

##### Cons:
- Complex relationships
	- Not as efficient for complex queries
- Consistency
	- May sacrifice ACID properties for scalability
	- Eventual consistency
- Language 
	- Query languages are not as mature as SQL

##### Use cases:
- Logging
- Blogs
- Web
- Analytics
- E-commerce
# XML
They can viewed as a type of document databases designed specifically storing, querying and manipulating data in the XML format. They are useful for small or medium sized databases

## Comparison

##### Pros:
- Handling complex XML data
- Flexibility
##### Cons:
- Can get slow
- Doesn't have strong consistency

##### Use cases:
- Application already uses XML
- XML pipelines
- Data for both machines and humans

##### Not good for:
- Big data
- Fast data transfer
- Highly connected data

# Key-value
One of the simplest database models. Data can only be made of Key-Value pairs. Each key needs to be unique; the value can either be a simple type (string, number) or a complex type (JSON).

## Performance
These databases are usually focusing on massive performance.