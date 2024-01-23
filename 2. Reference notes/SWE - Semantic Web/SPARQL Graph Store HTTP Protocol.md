Alternative to the SPARQL Update Protocol. Its purpose is to use HTTP operations for managing a collection of RDF graphs:
- GET - retrieve data (CONSTRUCT, SELECT)
- PUT - DROP/INSERT
- POST - INSERT
- DELETE - DROP

# GET
The query is part of the body of the request. Client specifies the format through Accept header.

```http
GET /rdf-graph-store?graph=<graph_uri> HTTP/1.1
Host: example.com
Accept: text/turtle; charset=utf-8

CONSTRUCT { ?s ?p ?o } WHERE { GRAPH <graph_uri> { ?s ?p ?o } }
```

# PUT
Send RDF data to replace a graph.

```http
PUT /rdf-graph-store?graph=<graph_uri? HTTP/1.1
Host: example.com
Content-Type: text/turtle

... RDF payload ...
```
same as:
```sparql
DROP SILENT GRAPH <graph_uri>;
INSERT DATA { GRAPH <graph_uri> { .. RDF payload .. } }
```

# DELETE
Specify a graph that should get deleted:

```http
DELETE /rdf-graph-store?graph=..graph_uri.. HTTP/1.1
Host: example.com
```

# POST
Insert a new graph to the dataset.

```http
POST /rdf-graph-store?graph=..graph_uri.. HTTP/1.1
Host: example.com
Content-Type: text/turtle

... RDF payload ...
```

[[SPARQL Update]]
[[2. Reference notes/SWE - Semantic Web/SPARQL|SPARQL]]