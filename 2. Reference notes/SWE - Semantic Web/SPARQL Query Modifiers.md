They allow for sorting, limiting, aggregating:
- ORDER BY - to sort either `DESC` or `ASC` based on a variable
- LIMIT - Restrict number of results returned
- OFFSET - Skip number of results
- GROUP BY - Group results based on specified variable(s)
- Aggregation functions - SUM, AVG, COUNT

```SPARQL
SELECT ?author (COUNT(?book) AS ?numBooks) WHERE {
	?book rdf:type ex:Book .
	?book ex:author ?author.
}
GROUP BY ?author
ORDER BY DESC(?numBooks)
LIMIT 10
OFFSET 0
```


[[_SWE Reference]]
[[SPARQL Query Language]]
[[SPARQL Select Query]]
[[SPARQL Pagination]]