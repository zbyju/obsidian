Designed for a more readable RDF format. Less verbose than RDF/XML.

It supports prefixes and base prefix:

```turtle
@prefix ex: <http://example.com/> .
```

Supports base prefix and prefix names:
```turtle
@base <http://baseprefix.org> .
@prefix otherPrefix: <http://otherPrefix.org/> .
```

Supports predicate lists by using `;`
```turtle
ex:
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