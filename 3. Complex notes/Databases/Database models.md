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

## Always indexed
There always needs to be a key present and it is the only way to query the data. There is no way to query based on value.

## Schema-less
There is no schema, any type of data can be stored as value.
## Comparison
##### Pros:
- Performance
- Scalability
- Simplicity
##### Cons:
- Limited functionality
- Very specific use cases

##### Use cases:
- Sessions
- Profiles
- Preferences
- Eshop cart

##### Not good for:
- Complex data
- Relations between data
- Complex queries


# Graph
Databases designed to simplify queries on a graph data. Data is in form of nodes but also relations. Both can be queried. It is powerful when querying based on the structure of the graph. Great for data with truly complex relations. They can be used to describe reality.

Graphs are Property graphs:
- Oriented
- Labeled
	- Nodes can have multiple labels
	- Edges can have only one label
- Multigraph
	- There can be more than one edge between two same nodes
- Nodes and edges have IDs
## Relationships
Relationships are first-class citizens. They are not just some foreign keys that link tables together but are a type of data themselves. They can have a type that can also be queried.

## Comparison
##### Pros:
- Efficient queries based on traversal of the graph
- Efficient queries based on relations
- They can be very flexible
##### Cons:
- Not as mature
- Can be slow for big datasets
- Features are not always useful

##### Use cases:
- Social networks
- Routing
- Location services
- User relationships

##### Not so good:
- Big datasets
- If relations are boring

# Wide-column
They organize data into columns, which are logically grouped. They allow efficient storage for large amounts of data and are great for distributed systems.

They have column family (instead of a table) which hold rows that can have similar columns (but not necessary the same).

There is usually just a handful of columns:
- Column name
- Column value
- Timestamp
Each datapoint has an id; then each row uses the id and then has the column name and value. 

## Schema flexible
They allow more in terms of schema flexibility than classical relational databases. Not every row has to have all columns specified.



#database-models
#key-value
#graph-database
#document-database
#xml-database
#key-value-database
#wide-column-database
#MongoDB 
#Cassandra
#Redis
#neo4j 


