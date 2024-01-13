There are several types of queries:
- SELECT
	- Extract raw values from a dataset
- CONSTRUCT
	- Creates new RDF graph based on the query pattern
- ASK
	- Returns a boolean indicating whether the query pattern exists in the data
- DESCRIBE
	- Returns RDF data about a resource

SPARQL again works with triples to form patterns that it looks for in the dataset.

It allows for:
- Filtering
- Sorting
- Limiting
- Skipping
- Aggregating
- Set operations
-  Prefixes and base prefixes:
	- PREFIX rdf: <...>
	- BASE <...>

# Predicate-Object Lists
Similarly to Turtle we can separate triples that have the same subject (and different predicate and object) by `;`

```sparql
?x  ext:name ?name ;
	ext:surname ?surname ;
	ext:nick ?nick ;
	ext:title ?title .
# same as
?x ext:name ?name .
?x ext:surname ?surname .
?x ext:nick ?nick .
?x ext:title ?title .
```

# Object Lists
Triples with the same subject and predicate (but different object) can be separated by `,`

```sparql
?x ext:nick "Honza", "Honzik", "Janek" .
```

# 'a' instead of 'rdf:type'
`a` 

[[_SWE Reference]]
[[2. Reference notes/SWE - Semantic Web/SPARQL|SPARQL]]
[[SPARQL Select Query]]