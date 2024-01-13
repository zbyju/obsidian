Designed for a more readable RDF format. Less verbose than RDF/XML.

It supports prefixes and base prefix:

```turtle
@prefix ex: <http://example.com/> .
```

# Example

```turtle
@prefix ex: <http://example.com/> .

ex:item a ex:Resource; ex:title "Example Item".
```
# Key components
1. RDF Graph
	- Using `rdf:RDF` tag
2. Subject
	- Using `rdf:Description` to declare a subject
	- Using `rdf:about` to specify URI
3. Predicate
	- Within the `rdf:Description` tag
	- Represented by the element name (title)
4. Object
	- Content of the predicate tag


[[_SWE Reference]]
[[RDF Formats]]
[[XML]]