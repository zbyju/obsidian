# Definitions
1. Database - repository for data we need to store
2. Schema - the columns of the database/table
3. ACID
	- Atomicity - All of the query either happens or it doesn't, not just partially
	- Consistency - The database is always in a state where all the contraints are satisfied
	- Isolation - Transactions don't effect each other
	- Durability - It needs to store the data successfully or fail
4. Transaction
	- Multiple queries to the database that are treated as a single thing

# NoSQL - Document based
## MongoDB
Database - multiple collections
Collection - multiple documents (~table)
Document (record) - BSON (JSON-like) data

