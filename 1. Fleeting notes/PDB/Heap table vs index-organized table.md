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
The heap table can also have an index implemented using a B* Tree.

![B Tree](https://i.imgur.com/rLkcdAZ.png)

