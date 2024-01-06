# Cost-based optimization
Technique used by the database engine (specifically the query optimizer) to determine the most efficient way to execute the query.

The goal is to minimize use of resources - time, disk I/O and memory.

# Execution Plan
Engine creates an execution plan - different strategies for retrieving the data. It calculates the cost for each execution plan and selects the plan with the lowest cost.

The execution plan is usually represented as a tree - each node represents some database operation - scan operations, different join operations (nested loops, hash join, merge join), sort, group, aggregation, filter operations.

The execution plans differ in:
- **Data access strategies** (full table scan vs index, etc.)
- **Different join operations** (nested loop join, hash join, merge join)
- **Order of operations**

# Statistics of Data Objects
The query optimizer uses statistics for cost calculation - it needs to know the sizes, distribution and characteristics of tables and indexes.

- **Data size, row count** - number of rows in a table or index, size of the table or index on disk
- **Data distribution**
	- Histograms 
	- Density values - proportion of table rows to be expected to have some value
- **Cardinality estimate** - number of distinct values in a column (high cardinality = many unique values, low cardinality = repeating values)
- **Index statistics** - Uniqueness and structure of indexes

Statistics are collected:
- **Automatically** - collecting in regular intervals or during certain operations
- **Manually** - admin can manually update the statistics

Statistics are used to estimate the cost. The optimizer uses the row counts to determine best scan approach and how big the result/sub-result will be. It uses the distribution statistics to estimate how many rows are going to get filtered out (when using `WHERE` or `JOIN`). 

Outdated statistics can be misleading. Statistics that are too simple might not capture the 