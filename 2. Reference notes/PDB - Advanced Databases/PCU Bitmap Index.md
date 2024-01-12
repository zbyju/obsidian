# Pros:
- Space efficient for repetitive data
- Quick retrieval
- Good for enumerated types (low cardinality)
- Good for OLAP

# Cons:
- Terrible for high cardinality (or normal cardinality)
- Slow for DML (insert, update, delete)

# Use cases:
- Making queries faster over low cardinality data

[[Bitmap Index]]
[[Database Index]]
[[Cardinality]]
#database-index 
#bitmap-index 