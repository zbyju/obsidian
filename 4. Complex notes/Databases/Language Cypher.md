It is a query language for interacting with graph databases (mainly Neo4j).

##### Pros:
- Intuitive syntax
- Easy to follow
- Graph data in mind
- Allows complex graph queries elegantly

##### Cons:
- Specific
- Learning curve

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

## Other clauses
- START
- MATCH
- WHERE
- RETURN
- ORDER BY
- SKIP
- LIMIT
- CREATE
- DELETE
- SET

#database-language
#database-cypher
#neo4j