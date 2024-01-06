# 1. Query parsing and syntax analysis
Take the query and parse it into a abstract syntax tree.

# 2. Semantic analysis
Check the query against the schema for correctness.

**Optimizations:** Schema information can be cached.

# 3. Query rewrite
Rewrite the query to optimize it further by simplifying some expressions, eliminating redundant subqueries, etc.


# 4. Query optimization
Generate several potential execution plans for the query and for each one calculate the cost. Pick the execution plan with the lowest cost.