# 1. Nested Loop Join
The simplest way of joining 2 tables is to for each row in the first table iterate over all rows in the second table.

##### Pros:
- Simple
- Most efficient for small tables or at least one table being small
- Efficient if the inner table is indexed on the join column ()