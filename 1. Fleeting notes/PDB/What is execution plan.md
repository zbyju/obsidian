Execution plan is a strategy of querying data. It describes the strategy of accessing the data, evaluating operations and ordering the operations. The database engine generates multiple such plans along with costs for each one; then picks the plan with lowest cost.

# How does it look like?
It can be represented in a tree structure - the root holds the final result and the nodes are database operations, leaves are data access.

# When is it created?
It's created with each query the database needs to handle.

## Ah-hoc queries
