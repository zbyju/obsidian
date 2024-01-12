# Pros:
- Faster lookup using the index key

# Cons:
- Takes more storage
- Slows down DML (insert, update, delete) 
	- They also need to update the index

# Use cases
- Primary key
- Optimizing queries
- Larger tables
- When a lookup by a specific key is expected

[[_PDB Reference]]
[[Heap table with index]]