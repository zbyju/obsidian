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

## Master-slave replication
Master database is replicated to slaves.

## Peer-to-peer replication
Each node has same standing and can read and write.

# Sharding
Splitting large dataset into smaller pieces called a shard. Each shard contains a subset of the dataset. It should improve scalability and performance of the database.

# Sharded Replication
Each shard is also replicated. Ensures scalability and high availability and fault tolerance.

# Strong vs Weak Consistency
## Strong Consistency
Uses ACID to maintain the database in a consistent state.
## Weak Consistency
= Eventual consistency
The data might not be consistent but are converging to be consistent at some point in the future.

## CAP
- If we want higher availability we need to settle for weak consistency
- If we want strong consistency we need to settle for lower availability

# Quorum
Quorum is a mechanism to ensure consistency and availability. It's a way to agree on a consensus among nodes about the current state of the dataset.

It's usually a majority vote that needs to agree and respond to a request for it to be successful.

If the quorum is not successful the request will fail.
## Write quorum
**W > N/2**
We need the majority to agree on a change. This will never lead to conflicts.

## Read quorum
**R > N - W** = R + W > N
We ask all nodes from read quorum and get the latest result (newest timestamp). This is enough because the write quorum agreed on the change.

# Big Data (3V+)
It's more of a buzzword, but there are characteristics:
- Volume
	- Data volume is increasing exponentially
- Variety
	- Various formats, types, structures
- Velocity
	- It's coming in quickly
	- Generated fast
	- Needs to be processed fast
- Veracity
	- There might be inconsistencies, incompleteness
- Value
	- Needs to be processed somehow to extract value

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
#eventual-availability
#quorum
#bigdata