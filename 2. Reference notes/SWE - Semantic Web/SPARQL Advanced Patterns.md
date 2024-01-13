# Optional
Specify that part of the matching pattern is optional. Useful for returning optional data - otherwise it would eliminate the whole entry.

```sparql
SELECT ?book ?title ?author WHERE {
	?book rdf:type ex:Book .
	OPTIONAL { ?book ex:title ?title . }
	OPTIONAL { ?book ex:author ?author . }
}
# get books
# if they have title and author specified
# then return them as well
```

# Union
Combine patterns together as a UNION (= logical or).

```sparql
SELECT ?title
WHERE {
	{ dbr:Czech_Republic rdfs:label ?title }
	UNION
	{ dbr:Czech_Republic foaf:name ?title }
}
```

[[_SWE Reference]]
[[SPARQL Select Query]]
[[SPARQL Query Language]]