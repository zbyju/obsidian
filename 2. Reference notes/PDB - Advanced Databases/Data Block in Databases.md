Understanding the data transfer between disk storage and RAM.
1. Data is stored on the disk.
2. Data is loaded from the disk into RAM.
	- Often, there's more data than available RAM.

- Heuristics aim to optimize data access, maximizing RAM usage.
- Databases use a "Database buffer cache".

- Data transfer occurs in blocks, typically around 8kB. If accessing a single row (e.g., 50B), the entire data block (e.g., 8kB) is loaded.

*Note:* Even if we want to access a single row (e.g. 50B in total), the database still needs to fetch the full block (8kB)

**Linkage:**
- [[_PDB Reference]]