![[Pasted image 20240106174949.png]]
# Heap table
Data gets inserted and assigned `ROWID`. There is no order in how the records are stored. Physical order in a heap cannot be predicted.

Pros:
- Inserting is quick
- There is no overhead managing an index
- Simple
Cons:
- Always needs a full table scan to access data
- Slow for bigger tables
- Fragmentation can lead to inefficiency

Use cases:
- Small tables
- When using an index is not worth it
# Heap table with index
The heap table can also have an index implemented using a B* Tree. Data is unordered in the heap.

![B Tree](https://i.imgur.com/rLkcdAZ.png)

All the internal (non-leaf) nodes guide the search - they include intervals to know which branch to take.
Leaf nodes store the data entries and pointers to the actual records in the heap table using `ROWID`. 

If we are using an index we have better lookup efficiency. Otherwise we still use the heap table.

Pros:
- Faster when using the index

Cons:
- Maintenance overhead for the index (when inserting, deleting, updating)
- Index takes additional storage

Use case:
- Useful for big tables
- When we know what column we are going to access by

# Index-Organized Table
Doesn't use the heap but rather stores everything within the B* Tree.

Intermediate leaves still just guide the traversal.
Leave nodes store the actual data, there are no pointers.

The data is ordered in the leaves.

Pros:
- Fast access using the index
- Space efficient - no separate index
- Can improve range based queries - data is sorted so we can sequentially get them

Cons:
- Overhead with index maintenance
- N