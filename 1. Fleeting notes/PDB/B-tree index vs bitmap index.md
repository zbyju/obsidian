# B-tree index
B-tree has data in its leaves, rest of the nodes are used for guiding the traversal. It is usually pretty wide and shallow.

##### Lookup
The index starts at the root and goes down following the branches according the key. The leaves contain either the value itself or a pointer to the value.

##### Insert/Delete
The index needs to be maintained with each insert and delete to maintain order and balance.

##### Pros
- Efficient for lookups by key
- Efficient for lookups by key range - the data is ordered by the key; there is a linked list between the leaves - we can find start and end leaves and then traverse the linked list to get the whole range
- Efficient for a lot of data
- Good for high cardinality
- Good for OLTP

Cons
- DML operations are expensive
- Not as efficient for low cardinality

Use case:
- Columns with high cardinality
- OLTP

# Bitmap index
Bitmap for each distinct value in the indexed column. The column gets split to as many columns as there are distinct values (Gender = Male, Female) and each column can either have value 0 or 1.

##### Lookup
To find all rows with a specific value, the database does bit operations to filter those rows.

##### Pros
- Space efficient - uses very little space for columns
- Fast - bit operations are fast
- Ideal for low cardinality columns (gender, enumerate types)
- Good for OLAP

##### Cons
- Really bad for high cardinality
- Very slow DML operations

##### Use case
- Columns with low cardinality
- OLAP