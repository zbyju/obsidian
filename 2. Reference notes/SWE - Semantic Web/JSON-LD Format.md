It is a method for encoding Linked Data in JSON. It is designed to be machine-readable. It is a W3C standard.

# Context
`@context`
Defines the scope and the vocabulary. It maps terms to URIs (so that we can later use them).
# Id
`@id`
Specifies the identifies of a node
# Value and type
`@value`, `@type`
Represents the data value of a property along with the type.

# Example
```turtle
@prefix ex: <http://example.org/>.
		ex:Alice a ex:Person;
		ex:knows ex:Bob;
		ex:email "alice@example.org".
```

```json
{
  "@context": {
    "ex": "http://example.org/",
    "Person": "ex:Person",
    "knows": "ex:knows",
    "email": "ex:email"
  },
  "@id": "ex:Alice",
  "@type": "Person",
  "knows": {"@id": "ex:Bob"},
  "email": "alice@example.org"
}
```
# Pros
- Compatible with JSON
- Easy to read and write
- Interoperability with other systems
# Cons
- Hard for humans to read

[[Web Annotations]]