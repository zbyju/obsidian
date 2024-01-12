# Pros:
- Makes JOINs more efficient
	- Related data are stored closely
- Better disk utilization
	- One read can get multiple data from multiple tables
		- Because they are in the same data block

# Cons:
- Performance degradation if used incorrectly

# Use cases
- Tables frequently joined together
- Tables frequently accessed together

[[_PDB Reference]]
[[Cluster Table]]