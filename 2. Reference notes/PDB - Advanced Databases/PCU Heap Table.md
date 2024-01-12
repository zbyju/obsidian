# Pros:
- Quick for DML (insert, update, delete)
- No overhead for managing an index
- Simple

# Cons:
- Full table scan is the only way to retrieve anything
- Slow lookup for big tables
- Potential degradation due to fragmentation

# Use cases:
- Small tables
- Tables where queries will return most of the data anyway
	- 