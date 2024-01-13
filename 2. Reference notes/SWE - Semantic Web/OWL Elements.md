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

# Disjoin classes
`owl:disjointWith`
There can be no individual that is an instance of both classes at the same time.

```turtle
:Man owl:disjointWith :Woman
```

# Advanced classes
`owl:intersectionOf` | `owl:unionOf` | `owl:complementOf`
Individual is an instance of both classes (intersection) or instance of at least one class(union) or instance of no class.

```turtle
:Mother owl:equivalentClass [
	a                  owl:Class ;
	owl:intersectionOf ( :Woman :Parent )
] .

:Parent owl:equivalentClass [
	a           owl:Class ;
	owl:unionOf ( :Father :Mother )
] .

:ChildlessPerson owl:equivalentClass [
	a                  owl:Class ;
	owl:intersectionOf ( 
		:Person
		[ a owl:Class ; owl:complementOf :Parent ]
	)
] .
```

# Comparing Individuals
`owl:sameAs` | `owl:differentFrom`
These can only be used on individuals.
They say 2 individuals are the same or different instances.

```turtle
:Jan owl:sameAs :Honza .
:Jan owl:differentFrom :Josef .
```

