- Consistency
	- All nodes see the same data at the same time.
- Availability
	- Even if one or more nodes are down, any client making a request receives a response.
- Partition Tolerance
	- In spite of any number of breakdowns in communication, the cluster will continue to work.
	- = Fault tolerance

CAP Theorem says that distributed databases can have at most 2 of 3 of these properties:
- CA
	- These databases aim for consistency and availability = all nodes have same data, and are available
	- If there is a breakdown then the rest continues to operate
	- PostgreSQL using replication
- CP
	- Consistency + partition tolerance = when there is a breakdown the system has to shutdown the inconsistent node (making it unavailable) until it's resolved 
	- MongoDB, Redis
- AP
	- Availability + Partition tolerance = when there is a breakdown all nodes remain available but those that are inconsistent might return older data.
	- Cassandra, RiakKV, DynamoDB

[[_PDB Reference]]
[[2. Reference notes/PDB - Advanced Databases/NoSQL|NoSQL]]
[[Horizontal Scaling]]
