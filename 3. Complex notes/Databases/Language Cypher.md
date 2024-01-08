It is a query language for interacting with graph databases (mainly Neo4j).

# Main features
## Graph pattern matching
`()` - nodes
`<--` | `--` | `-->` - relationships

```cypher
(node1)-[relationship]->(node2)
```

## Chaining
Clauses can be chained together

## Match Clause
```cypher
MATCH (i:ACTOR)<-[:PLAY]-(m:MOVIE)-[:PLAY]->(a:ACTOR)
	WHERE (i.name = "Ivan Trojan")
RETURN a.name
```


#database-language
#language-cypher