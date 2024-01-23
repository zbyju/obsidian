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
ex:john ex:friendOf ex:jane;
		ex:enemyOf  ex:joe .
```

Uses token `a` for rdf:type

Uses `[]` for blank nodes:
```turtle
ex:john ex:friendOf [
	ex:firstname "Jane" ;
	ex:lastname "Doe"
] .
```
# Example

```turtle
@prefix ex: <http://example.com/> .

ex:item a        ex:Resource;
		ex:title "Example Item".
```


[[RDF Formats]]
[[RDFXML Format]]