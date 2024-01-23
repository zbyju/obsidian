It is used to extract information from RDF dataset and transform the result into a new RDF graph.

They are made up of several parts:
- CONSTRUCT - how the result should look like
- WHERE - the pattern to match against

```sparql
CONSTRUCT { ?person foaf:name ?name }
WHERE { ?person ext:name ?name }
# translate ext:name to foaf:name
```

[[SPARQL Query Language]]