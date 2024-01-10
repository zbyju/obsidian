# CAP
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
## Vertical scaling
We add computing power. It might get expensive to scale like this. Good for strong consistency.
##### Pros:
- Simple
- No need to deal with distributed systems
- Consistency
##### Cons:
- Might get really pricy
- Vendor lock-in
- Cannot be applied indefinitely
## Horizontal scaling
Adding more nodes.

##### Pros:
- Less expensive
- Theoretically unlimited scaling
##### Cons:
- Complex solution
- Consistency problems
- Synchronization
- Infrastracture

CAP explains the problems with horizontal scaling and the difficulties and trade-offs we have to make. We need to either choose consistency or availability.

# ACID
Focus on CA
- Atomicity
	- Transaction is either successful or fails
- Consistency
	- Write can be completed only when all they pass all constraints
- Isolation
	- Transactions don't effect each other
- Durability
	- Once the changes are confirmed they are persistently stored

# BASE
Focus on AP
- Basically Available
	- The system is always available (as a unit)
- Soft-state
	- The state of the system may change over time (even without input). After write we might still read old data.
- Eventually consistent
	- System will be consistent at some point in the future
	- But might not be at all times

# Replication
Creating copies of the database (or portions of the database) and storing them on different nodes.

Main purpose is to increase availability and fault tolerance and reduce load on the primary database.


#CAP 
#ACID
#BASE
#distributed-systems
#scaling
#horizontal-scaling
#vertical-scaling
#database-consistency
#database-availability
#database-partition-tolerance
#sharding
#replication
