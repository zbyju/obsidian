# Database statistics
- Row Count
- Pages Count
- Data Distribution
	- Min, Max
	- Histograms
- Block Factor
	- Average number of rows in one block
- Cardinality

They are not updated with each DML operation, but rather automatically, when the database is not busy (or manually).
# B-tree statistics
- Depth
	- Typically 2-3
- Branching Factor
	- Typically (50-150)
- Number of Leaves
- Clustering Factor
	- Measures how the order of the idnexe
- Average Key Length
- Distinct Keys
- Index Density

