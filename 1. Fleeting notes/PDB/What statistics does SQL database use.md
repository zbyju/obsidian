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
	- Amount of data blocks that must be visited to receive 
	- Measures how the order of the index correlates with the order of the table data. 
	- Low clustering index = data on disk are stored in close proximity to how the index is sorted
		- Leads to better performance
	- High clustering index = data close to each other in index are stored far away on disk
- Average Key Length
- Distinct Keys
- Index Density

