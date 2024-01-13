Enable execution of a single query across multiple endpoints. It allows us to query and combine data from different sources.

Keyword `SERVICE` is used to tell SPARQL it should get the information from a different endpoint.

```sparql
SELECT ?title ?author WHERE {
	SERVICE <http://example.org/sparql> { ?book rdf:type ex:Book. ?book ex:title ?title. ?book ex:author ?author. } }
```