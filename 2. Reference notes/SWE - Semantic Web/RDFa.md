RDFa is used to embed RDF into XHTML as it defined number of extension attributes for it to work.

Important syntax:
- rel
- property
- datatype


When a subject is not defined then it is assumed to be the URI of the document itself:
# rel
Is used to reference external sources (using `href`)

```html
Content on this page is licensed under
<a  xmlns:ext="http://www.example.org/terms"
	rel="ext:license"
	href="http://creativecommons.org/license/by/3.0">
a Creative Commons License &ndash; attribution
</a>
```
same as:
```turtle
<http://blog.dojchinovski.mk/?p=107> ext:license <http://creativecommons.org/license/by/3.0> .
```

# property
Is used for literals.
```html
<div xmlns:dc="http://purl.org/dc/elements/1.1/">
	<h3 property="dc:creator">Milan<h3>
</div>
```
same as:
```turtle
<http://blog.dojchinovski.mk/?p=107> dc:creator "Milan" .
```

# Typed literals
```html
<div xmlns:dc="http://purl.org/dc/elements/1.1/"
	 xmlns:xsd="http://www.w3.org/2001/XMLSchema#">
	<h3 property="dc:creator" datatype="xsd:string">Milan<h3>
</div>
```