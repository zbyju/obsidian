# Cost-based optimization
Technique used by the database engine (specifically the query optimizer) to determine the most efficient way to execute the query.

The goal is to minimize use of resources - time, disk I/O and memory.

# Execution Plan
Engine creates an execution plan - different strategies for retrieving the data. It calculates the cost for each execution plan and selects the plan with the lowest cost.

The execution plan is usually represented as a tree - each node represents some database operation - scan operations, different join operations (nested loops, hash join, merge join), sort, group, aggregation, filter operations.

The execution plans differ in:
- Data access strategies (full table scan vs index, etc.)
- Different join operations (nested loop join, hash join, merge join)
- Order of operations

# Statistics of Data Objects
The query optimizer uses statistics for cost calculation - it needs to know the sizes, distribution and characteristics of tables and indexes.

- Data size, row count
- Data distribution