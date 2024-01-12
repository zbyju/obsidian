Helps quickly locate data without having to go through the whole database. It's a tradeoff between quick retrieval and slower insert/update/delete.

It works by using specific data structures that have faster lookup times. These data structures need to be maintained, when changes to the dataset happen.

# Pros:
- Quicker lookup

# Cons:
- Slower DML (insert, update, delete)
- Consumes extra storage

[[_PDB Reference]]
[[B Tree]]
[[B+ Trees in Databases]]
[[index]]