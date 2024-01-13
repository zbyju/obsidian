The SPARQL specifies a protocol built on top of HTTP and supports 2 operations:
- Query - send a SPARQL query to the endpoint and receive results
- Update - send a SPARQL update request to a service


Requests are sent using HTTP GET or POST:
- GET
- POST URL-encoded
- POST directly

Results are returned in a selected format: XML, CSV, JSON, Turtle, RDF/XML, N-triples, JSON-LD.

# GET
It is submitted as part of a query string parameter:

