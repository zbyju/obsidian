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



[[_SWE Reference]]
[[2. Reference notes/SWE - Semantic Web/SPARQL|SPARQL]]
[[SPARQL Select Query]]