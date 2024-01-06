# 1. Query parsing and syntax analysis
Take the query and parse it into a abstract syntax tree.

# 2. Semantic analysis
Check the query against the schema for correctness (also check user permissions)

**Optimizations:** Schema information can be cached.

# 3. Query rewrite
Rewrite the query to optimize it further by simplifying some expressions, eliminating redundant subqueries, etc.


# 4. Query optimization
Generate several potential execution plans for the query and for each one calculate the cost. Pick the execution plan with the lowest cost.

# 5. Execute the plan
Run the query according to the best execution plan and return the result.

- The execution starts with accessing the data sources using chosen data access methods
- In the middle layers, there are basic relational operations (selec)