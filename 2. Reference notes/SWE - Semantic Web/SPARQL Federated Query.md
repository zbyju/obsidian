Enable execution of a single query across multiple endpoints. It allows us to query and combine data from different sources.

Keyword `SERVICE` is used to tell SPARQL it should get the information from a different endpoint.

```sparql
SELECT ?title ?author WHERE {
	?book rdf:type ex:Book.
	SERVICE <http://example.org/sparql> {
		?book ex:title ?title.
		?book ex:author ?author. 
	}
}

SELECT ?person ?interest ?known WHERE {
	SERVICE <http://people.example.org/sparql> {
		?person foaf:name ?name .
		OPTIONAL {
			?person foaf:interest ?interest . #optional
			SERVICE <http://people2.example.org/sparql> {
				?person foaf:knows ?known . #optional
			}
		}
	}
}
```