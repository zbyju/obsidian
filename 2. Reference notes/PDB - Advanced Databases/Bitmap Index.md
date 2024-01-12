Bitmap index uses a simple map of bits for each unique value in a column, optimizing for space and retrieval speed.

# Characteristics
- Each unique value is a new column
- There are 0 or 1 bits in the columns
- Bit operations are used for lookup

# Example
Gender:
```
Name | Male | Female
--------------------
John | 1    | 0
Jane | 0    | 1
```