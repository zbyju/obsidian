There is one master that controls one or more slave components. Master sends requests to the slaves which return a response to the master. It is often used to simplify processes, distribute workload, manage tasks.

# Use Cases
- Database Replication
	- Master replicates all data to slaves
	- Master is the only one that can handle update requests
	- Slaves can handle read requests on their own
- Load Balancing
- Parallel Processing

# Pros
- Efficiency
- Scalability
- Fault Tolerance (over slaves)

# Cons
- Single point of failure
- Complexity
- Scalability limits (due to one master)

[[Architectures]]