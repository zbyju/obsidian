The optimizer generates multiple execution plans based on available indexes, access paths. Then picks the one with lowest cost.

# When is full table scan better than index scan?
1. Small tables
	- If tables are small than going through the index can be slower
2. High selectivity
	- If most records are returned anyway, then using an index doesn't save time

#database-execution-plan 