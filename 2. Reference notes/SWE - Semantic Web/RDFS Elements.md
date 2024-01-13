# Classes
`rdfs:Class`
Groups resources by similar characteristics.

```turtle
:Book rdf:type rdfs:Class .
```

# Subclass Relationships
`rdfs:subClassOf`
Enables hierarchical organization of classes.

```turtle
:Novel rdfs:subClassOf :Book .
```

# Properties
`rdfs:Property`
Define properties, which are relationships between resources.

```turtle
:author rdf:type rdfs:Property .
```

# Subproperty Relationships
`rdfs:subPropertyOf`
Enables hierarchical organization of properties

```turtle
:bookAuthor rdfs:subPropertyOf :author .
```

# Domain and Range
`rdfs:domain` and `rdfs:range`
To define what subject the property can be used with (domain) and the what values it can have (range).

```turtle
:author rdfs:domain :Book   ;
		rdfs:range  :Person .
```

# Utility
`rdfs:label`  (but also others: `rdfs:comment`, `rdfs:seeAlso`, `rdfs:isDefinedBy`)

```turtle
:Book rdfs:label "My Book" .
```


[[_SWE Reference]]
[[RDF Schema]]
[[RDF Resource]]