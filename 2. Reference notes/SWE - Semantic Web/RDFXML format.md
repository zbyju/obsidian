RDF/XML is a format that utilizes XML for representing RDF graphs.

```xml
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
	<rdf:Description rdf:about="http://example.com/item">
		<title>Example Item</title>
	</rdf:Description>
</rdf:RDF>
```

It is difficult to read.
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