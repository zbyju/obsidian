It is a NoSQL database for fast product catalog applications (ecommerce, eshops, ...). It's main focus is on low latency.

# All indexes in RAM
All indexes remain in RAM to allow for fast parallel read without locks.

# Smart Cache
The database engine has a smart cache - no needs for an application cache or other complicated solutions.

EvitaDB uses immutable data structures therefore the cache will always have up-to-date data.

# GraphQL, REST, gRPC API
EvitaDB offers GraphQL, REST and gRPC API out of the box. This helps close the gap between frontend and backend developers to communicate.

# ACID
The database works in 2 regimes:
1. Initialization - optimized for fast write to initialize the data
2. Standard - optimized for reads, now supports ACID.

##### Pros:
- Fast
- Low latency
##### Cons:
- Optimized for Ecommerce


#database-models 
#evitadb
#ecommerce 