# Classes
`owl:Class`
For class definition.

```turtle
:Person rdf:type owl:Class .
```
# Equivalent classes
`owl:equivalentClass`
Some vocabulary classes can be the same, but use a different identifier. We can express that these identifiers represent the same thing.
It's same as saying `rdfs:subClassOf` 2 times in both directions.

```turtle
:Person owl:equivalentClass :Human
```