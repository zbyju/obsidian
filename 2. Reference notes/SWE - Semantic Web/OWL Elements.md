# Classes
`owl:Class`
For class definition.

```turtle
:Person rdf:type owl:Class .
```
## Equivalent classes
`owl:equivalentClass`
Some vocabulary classes can be the same, but use a different identifier. We can express that these identifiers represent the same thing.
It's same as saying `rdfs:subClassOf` 2 times in both directions.

```turtle
:Person owl:equivalentClass :Human
```

## Disjoin classes
`owl:disjointWith`
There can be no individual that is an instance of both classes at the same time.

```turtle
:Man owl:disjointWith :Woman
```

## Advanced classes
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

## Comparing Individuals
`owl:sameAs` | `owl:differentFrom`
These can only be used on individuals.
They say 2 individuals are the same or different instances.

```turtle
:Jan owl:sameAs :Honza .
:Jan owl:differentFrom :Josef .
```

# Property
`owl:ObjectProperty` | `owl:DatatypeProperty`
Object properties where object is a resource.
Datatype property where object is a literal

```turtle
:hasWife a           owl:ObjectProperty ;
		 rdfs:domain :Man               ;
		 rdfs:range  :Woman             .

:hasAge a           owl:DatatypeProperty   ;
		rdfs:domain :Person                ;
		rdfs:range  xsd:nonNegativeInteger .
```

## Negative Object Property
`owl:NegativePropertyAssertion`, `owl:sourceIndividual`, `owl:assertionProperty`, `owl:targetIndividual`
States that 2 individuals are not connected by a property.

```turtle
# Bobs wife is not Mary
[]  a                     owl:NegativePropertyAssertion ;
	owl:sourceIndividual  :Bob ;
	owl:assertionProperty :hasWife ;
	owl:targetIndividual  :Mary .
```

## Property Restrictions
`owl:Restriction`, `owl:onProperty`, `owl:someValuesFrom` | `owl:allValuesFrom` | `owl:hasValue`
We can specify quantification restrictions - existential and universal quantification or it must have a constant value.

### Cardinality
`owl:maxQualifiedCardinality` | `owl:minQualifiedCardinality` | `owl:qualifiedCardinality` | `owl:cardinality`

We can specify the max and min cardinality of a property.
Or an exact cardinality

## Property Relationships
`owl:inverseOf` | `owl:equivalentProperty` | `owl:TransitiveProperty` | `owl:SymmetricProperty` | `owl:AsymmetricProperty` | `owl:FunctionalProperty` | `owl:InverseFunctionalProperty` | `owl:ReflexiveProperty` | `owl:IrreflexiveProperty`

### inverseOf
One property is an inverse of another.

```turtle
:hasChild owl:inverseOf :hasParent .
```

### equivalentProperty
States that 2 properties are the same one with a different name.

```turtle
:hasChild owl:equivalentProperty :child
```

### Relation Properties
Describe the type of relation there is between individuals with this property.

```turtle
# Transitive (Prague is transitively in CZ)
:isLocatedIn a owl:TransitiveProperty .
:Prague :isLocatedIn :CentralBohemia .
:CentralBohemia :isLocatedIn :CZ .
# => :Prague :isLocatedIn :CZ

# Symmetric (Being a friend goes both ways)
:hasFriend a owl:SymmetricProperty .

# Asymmetric (Parent cannot be a child of its children)
:hasChild a owl:AsymmetricProperty .

# Reflexive (Everybody is a relative of himself)
:hasRelative a owl:ReflexiveProperty .

# Irreflexive (Nobody is its own parent)
:hasParent a owl:IrreflexiveProperty .

# Functional (if a subject has 2 different objects
# through this relation
# then that object has to be the same instance
# )
:hasHusband a           owl:FunctionalProperty .
:Mary       :hasHusband :John .
:Mary       :hasHusband :James .
# => John == James

# Inverse functional (if an object has
# 2 different subjects pointing to it
# throught a inverse functional relation
# then those 2 subjects are the same.
#)
:isMother a owl:InverseFunctionalProperty .
:Jane     :isMother :John .
:Janet    :isMother :John .
# => Jane == Janet
```




[[OWL]]
[[RDF Schema]]
[[RDFS Elements]]
[[RDF Resource]]
[[RDF Literal]]
[[RDF Object]]