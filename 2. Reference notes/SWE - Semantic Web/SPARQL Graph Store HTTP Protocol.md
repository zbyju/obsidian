Alternative to the SPARQL Update Protocol. Its purpose is to use HTTP operations for managing a collection of RDF graphs:
- GET - retrieve data (CONSTRUCT, SELECT)
- PUT - DROP/INSERT
- POST - INSERT
- DELETE - DROP

# GET
The query is part of the body of the request. Client specifies the format 

```http
GET /rdf-graph-store?graph=<graph_uri> HTTP/1.1
Host: example.com
Accept: text/turtle; charset=utf-8

CONSTRUCT { ?s ?p ?o } WHERE { GRAPH <graph_uri> { ?s ?p ?o } }
```