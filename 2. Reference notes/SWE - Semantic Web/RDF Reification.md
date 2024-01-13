Method of representing metadata about statements.
- = Statements about statements
- = Statements where the subject is another statement

RDF in it self support this using blank nodes and `rdf:Statement`, `rdf:subject`, `rdf:predicate`, `rdf:object`.

```turtle
_:statement rdf:type rdf:Statement .
_:statement rdf:subject :Tolkien .
_:statement rdf:predicate :wrote .
_:statement rdf:object :LordOfTheRings .

_:statement :source :Wikipedia
```


[[_SWE Reference]]
[[2. Reference notes/SWE - Semantic Web/RDF|RDF]]
[[RDF Statement]]
[[RDF Subject]]