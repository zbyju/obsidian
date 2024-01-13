Update language for RDF. Uses same syntax as SPARQL Query Language ([[SPARQL Query Language]]). 

Operations for:
- insert triples (`INSERT DATA`)
- delete triples (`DELETE DATA`)
- load RDF graphs
- clear RDF graphs
- create RDF graphs
- drop RDF graphs
- copy, move, add triples from one graph to another
- execute group of update operations


# Insert
```sparql
INSERT DATA {
	GRAPH <http://example/bookStore> {
		<http://example/book1> dc:title "A new book" ;
		dc:creator "A.N.Other" .
	}
}
```

`GRAPH` is optional. `INSERT` doesn't create a new graph.

# Delete
```sparql
DELETE DATA {
	GRAPH <http://example/bookStore> {
		<http://example/book1> dc:creator "A.N.Other" .
	}
}

DELETE { ?book ?p ?v } WHERE {
	?book dc:date ?date .
	FILTER ( ?date > "1970-01-01T00:00:00-02:00"^^xsd:dateTime )
	?book ?p ?v
}
```