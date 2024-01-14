It's a language for describing and validating RDF graphs against constraints.

It uses these terms:

# Shape
Defines how to validate a *Focus Node* based on values of properties.

# Focus Node
RDF term that is validated against a Shape (URI, literal, blank node). They are the target of a shape.

# Node Shape
Specifies constraints that need to be met with respect to Focus Nodes. 
(Directly on the node)

```turtle
ex:ExampleNodeShape a sh:NodeShape ;
	sh:property [
		sh:path ex:email ;
		sh:name "e-mail" ;
		sh:description "We need at least one email value" ;
		sh:minCount 1 ;
	] .
```

# Property Shape
Specify constraints that need to be met with respect to properties of the focus node.
(Connected to the node)

```turtle
ex:ExamplePropertyShape a sh:PropertyShape ;
	sh:path ex:email ;
	sh:description "We need at least one email value" ;
	sh:minCount 1 .
```
# Targets
Triples with the shape as the subject + properties described as predicates.
They are used to produce focus nodes for a shape.

# Constraints
Conditions that are checked for validity.


[[_SWE Reference]]
[[2. Reference notes/SWE - Semantic Web/RDF|RDF]]
[[Advanced SHACL]]
[[SHACL vs ShEx]]