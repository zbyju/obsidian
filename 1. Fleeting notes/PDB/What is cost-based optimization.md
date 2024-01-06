Technique used by the database engine (specifically the query optimizer) to determine the most efficient way to execute the query.

The goal is to minimize use of resources - time, disk I/O and memory.

Engine creates an execution plan - different strategies for retrieving the data. It calculates the cost for each execution plan and selects the plan with the lowest cost.

The execution plan is usually represented as a tree - each node represents some database operation - scan operations