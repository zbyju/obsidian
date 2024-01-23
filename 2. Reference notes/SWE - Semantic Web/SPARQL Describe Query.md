Used to extract triples describing certain resources found to match a pattern. It often results in the SPARQL query processor to return all the results where the resource appears as a subject.

```sparql
DESCRIBE ?book WHERE {
	?book rdf:type ex:Book .
}
```


[[SPARQL Query Language]]