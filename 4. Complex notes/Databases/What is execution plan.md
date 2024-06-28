Execution plan is a strategy of querying data. It describes the strategy of accessing the data, evaluating operations and ordering the operations. The database engine generates multiple such plans along with costs for each one; then picks the plan with lowest cost.

# How does it look like?
It can be represented in a tree structure - the root holds the final result and the nodes are database operations, leaves are data access.

# When is it created?
It's created with each query the database needs to handle.

## Ah-hoc queries
Queries that are submitted on-the-fly, the execution plan is generated every time such query is submitted to the database.

## Prepared statements
For prepared statements, the execution plan may already be generated from before and reused for subsequent queries.

# Is it worth caching it?
Depending on the situation it is a good idea to cache it, but it can be tricky.

##### Pros:
- Better performance
- Really good if the same query repeats a lot
##### Cons:
- If the underlying data changes significantly, it needs to be recalculated
- Certain execution plan can be optimized for a certain set of parameters

#database-execution-plan 
#database-prepared-statement