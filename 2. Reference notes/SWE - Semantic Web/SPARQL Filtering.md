We can use `FILTER` to add constraints on the variables based on logical comparisons (`= != < >`) or even regex `regex(variable, pattern)` and other functions.

```SPARQL
SELECT ?person ?name ?country ?population WHERE {
	?person a dbo:Person .
	?person rdfs:label ?name .
	?person dbo:birthPlace ?country .
	?country dbo:populationTotal ?population .
	
	FILTER (langMatches( lang(?name), "en" ) )
	FILTER (?population > 1000000)
}
```


[[_SWE Reference]]
[[SPARQL Query Language]]
[[SPARQL Select Query]]