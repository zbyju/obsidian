Used for providing information about resources

Resource is anything that can be conveyed electronically, or any abstract concept.

subject - predicate - object

subject = thing the statement describes
predicate = property of the object
object = value of the property

We use graph notation for representation
- Labeled, directed graph subject -> object
- Nodes are subjects and objects
	- Circles are resources
	- Rectangles are literals
- Edges are predicates

There are machine friendly languages:
- RDF/XML, Turtle, N-triples, JSON-LD

Triples are statements
IRIs for identifying resources
Literals are basic values
Blank nodes are for n-ary relationships, they are not referenced from outside the graph, _:ID, they are only locally unique
RDF graph - set of statements

URIref = URI + optional fragment identifier (http://example.com/people#me)
Set of URIrefs are RDF vocabulary

