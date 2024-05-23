**Textové a bag-of-words modely pro vyhledávání podle obsahu. Podobnostní model vyhledávání, podobnostní míry a dotazy.**

# Text based model
Useful for other media retrieval too (images, videos, sounds, ...) if we have a text description of those media files.

Terminology:
- Collection = set of all documents ($d_j$ - document with index j; there are n documents)
- Vocabulary = set of all terms in collection ($t_i$ - term with index i; there are m terms (usually 10,000-100,000))
- Document = some text (usually 100-1000 terms)
	- Unordered set of terms ($d_j = \{t_{i1}, t_{i2}, t_{i3}, ..., t_{ik}\}$ )
- Query = query document or set of keywords (usually 10)

- Input = any text
- Preprocessing:
	- Remove unwanted characters (HTML tags, punctuation, numbers, ...)
	- Break into words
	- Simplify terms (lematization, stemming)
	- Remove stop words
	- => Index Terms (result)

# Bag of Features

