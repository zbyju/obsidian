These patterns improve how we model our data.
We should definitely try to reuse existing data models (RDFS, OWL).
# Custom datatype
If we are missing a datatype (from XSD for example), we can create our own datatype and publish it.

# Index resources
We can use rdf:List or rdf:Seq to create a list of resources.

# Label everything
Provide names for every resource using `rdfs:label`.

# Link NOT label
Literals are not linkable, they are the leaves of our graph => don't use them for resources, instead provide an URI for resources.

# Multilingual labels
Provide labels in different languages using `resource rdfs:label "Praha"@cs, "Prague"@en.`

# N-ary relationships
Breakdown n-ary relationships into binary relationships.

```turtle
ex:milan ext:address ex:milansAddress .
ext:milansAddress    ext:street "Thakurova" ;
					ex:city ex:Prague ;
					ex:zip "160 00";
```

# Quantified relationships
Annotate relationships by creating a resource for it and then providing metadata for it.

```turtle
_:bobMaryMarriage    a ex:Marriage;
					ex:partner eg:bob;
					ex:partner eg:mary;
					ex:date "2009-04-01"^^xsd:date.
```

# Reified statement
Make statements about statements to provide metadata.

# Repeated properties
If we have a property with multiple values then we should use the same subject and property with a different object.

[[Linked Data Patterns]]