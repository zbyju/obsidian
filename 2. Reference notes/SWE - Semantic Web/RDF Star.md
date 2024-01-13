Extends RDF with a convenient way to make statements about other statements.

It can have triple as a subject or an object.

Uses `<< statement >>` syntax.

```turtle
<< :John :shot :Joe >> :accordingTo :Jane .
<< :Joe :shot :John >> :accordingTo :Jill .
```