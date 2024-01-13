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
To define the domain 