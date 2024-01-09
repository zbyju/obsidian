# Relational
Classical database model with the deepest history and most versatility.

# Document
Data stored as documents - JSON, BSON, XML or similar formats. Each documents is a self-contained unit and can have a different structure. This allows for a more natural and intuitive data representation.

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