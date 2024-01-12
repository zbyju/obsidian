# Pros
- Faster than normal heap table
	- There is no need to follow the pointer that is in the leaf
- Saves space
	- No need to have a separate data structure for data and index
- Enhanced performance for ranged queries
	- Data is next to each other in the B* tree
	- But they can be anywhere in the heap table

# Cons:
- Only works efficiently with 1 index
- Slower DML

# Use cases:
- Large tables
- Access by primary key only
- Access by one key only

[[_PDB Reference]]
[[Index Organized Table]]
[[Heap table]]
[[Heap table with index]]