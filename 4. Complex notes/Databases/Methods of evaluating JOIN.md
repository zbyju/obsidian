# 1. Nested Loop Join
The simplest way of joining 2 tables is to for each row in the first table iterate over all rows in the second table.

##### Pros:
- Simple
- Most efficient for small tables or at least one table being small
- Efficient if the inner table is indexed on the join column
##### Cons:
- Can be very slow for large tables

##### Use case:
- Outer table is small
- Inner table is indexed on the join column

# 2. Hash Join
Build a hash table on the join key. Compare groups with same hash value.

##### Pros:
- Faster than nested loops
##### Cons:
- Requires memory to hold the hash table

##### Use case:
- Fast for big tables

# 3. Merge Join
Both tables are sorted according to the join key and then merged. Usually doesn't fit into memory => need more runs (read-sort-write multiple times)

##### Pros:
- Efficient for tables that are already sorted on join key.
- Performs well on large datasets
##### Cons:
- Sort can be costly
- Requires a lot of memory

##### Use case:
- Large datasets
- Datasets already sorted on join key

# Special Join
- Index Join
- Hash cluster join
- ...

#database-join