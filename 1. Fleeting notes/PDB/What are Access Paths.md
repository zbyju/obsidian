They are different strategies for accessing the data from the database. Access paths will greatly impact the query performance.

- Full table scan
- Index scan

`SELECT * FROM R WHERE A = 'x'`

1. No index = full table scan
	- if A is unique then on average the cost is: $pR/2$
	- if A in not unique then the cost is: $pR$
2. Unique index = index scan
	- in case of heap table the cost is: $I(A,R) + 1$
	- in case of IOT the cost is: $I(A,R)$
3. Non-uniqeu index = index scan
	1. 