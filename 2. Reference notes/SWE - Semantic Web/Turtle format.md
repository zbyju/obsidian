Designed for a more readable RDF format. Less verbose than RDF/XML.

It supports prefixes and base prefix:

```turtle
@prefix ex: <http://example.com/> .
```

# Example

```turtle
@prefix ex: <http://example.com/> .

ex:item a        ex:Resource;
		ex:title "Example Item".
```


[[_SWE Reference]]
[[RDF Formats]]
[[RDFXML Format]]