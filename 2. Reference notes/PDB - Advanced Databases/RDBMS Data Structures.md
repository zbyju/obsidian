Different structures in a relational database management system (RDBMS).
- Heap table: A random data collection, no guaranteed order.
- Heap table with index: Similar, but with an index for data access, typically implemented using a B* tree or bitmap.
  - Not wise to index everything as it speeds up SELECT but slows down INSERT, UPDATE, DELETE.
	  - There is overhead in maintaining the index
- Index organised table: Instead of pointers, the actual data is stored.
- Cluster: Data is grouped into buckets.
	- E.g., employees grouped by department.

- Each record has a unique rowid describing its physical path.
  - Can be used for a SELECT but might change; therefore, not recommended.
  - Used in index implementation.

**Linkage**:
- [[B* Trees in Databases]]
- [[Access Methods in Databases]]