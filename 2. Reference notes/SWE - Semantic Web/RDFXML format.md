RDF/XML is a format that utilizes XML for representing RDF graphs. It can be difficult to read.

```xml
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
	<rdf:Description rdf:about="http://example.com/item">
		<title>Example Item</title>
		<blankNode rdf:nodeId="blankNodeExample1" />
	</rdf:Description>

	<rdf:Description rdf:nodeId="blankNodeExample1">
		<test>Test</test>
	</rdf:Description>
</rdf:RDF>
```

We can add prefixes by using `xmlns:prefix=""` to the `rdf:RDF` tag, or `xml:base` for a default prefix.
# Key components
1. RDF Graph
	- Using `rdf:RDF` tag
2. Subject
	- Using `rdf:Description` to declare a subject
	- Using `rdf:about` to specify URI
	- Using `rdf:nodeId` to reference a node
1. Predicate
	- Within the `rdf:Description` tag
	- Represented by the element name (title)
2. Object
	- Content of the predicate tag
	- Using `rdf:nodeId` to reference a node


[[RDF Formats]]