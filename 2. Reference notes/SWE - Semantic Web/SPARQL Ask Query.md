It is used to check if a given pattern is present in the dataset. The result of this query is either true of false. They are used for simple checks.

```sparql
ASK {
	?x foaf:name "Alice" ;
	foaf:mbox <mailto:alice@work.example> .
}
```

[[_SWE Reference]]
[[SPARQL Query Language]]