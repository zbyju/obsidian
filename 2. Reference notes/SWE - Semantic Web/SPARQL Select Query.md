It is used to extract specific data from a dataset. It uses a similar syntax to Turtle for describing triples.

Syntax:
- Variables are prefixed with ?
- Pattern to be returned is after SELECT clause
- Pattern to be matched is after WHERE clause

```SPARQL
SELECT ?subject ?predicate ?object WHERE {
	?subject ?predicate ?object .
}

SELECT ?person ?name ?country ?population WHERE {
	?person a dbo:Person .
	?person rdfs:label ?name .
	?person dbo:birthPlace ?country .
	?country dbo:populationTotal ?population .
}
```

[[Turtle Format]]
[[SPARQL Query Language]]