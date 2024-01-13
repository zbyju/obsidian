# Optional
Specify that part of the matching pattern is optional.

```sparql
SELECT ?book ?title ?author WHERE {
	?book rdf:type ex:Book. OPTIONAL { ?book ex:title ?title. } OPTIONAL { ?book ex:author ?author. } }
```