The SPARQL specifies a protocol built on top of HTTP and supports 2 operations:
- Query - send a SPARQL query to the endpoint and receive results
- Update - send a SPARQL update request to a service


Requests are sent using HTTP GET or POST:
- GET (only for query)
- POST URL-encoded
- POST directly

Results are returned in a selected format: XML, CSV, JSON, Turtle, RDF/XML, N-triples, JSON-LD.

# GET
It is submitted as part of a **query** string parameter:

```sparql
PREFIX dc: <http://purl.org/dc/elements/1.1/>
SELECT ?book ?who
WHERE { ?book dc:creator ?who }
# =>
GET /sparql/?query=PREFIX%20dc%3A%20%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Felements...
Host: www.example.org
User-agent: my-sparql-client/0.1
```

# Direct POST
The query is submitted as a body of the request.

```sparql
PREFIX dc: <http://purl.org/dc/elements/1.1/>
SELECT ?book ?who
WHERE { ?book dc:creator ?who }
# =>
POST /sparql/
Host: www.example
User-agent: sparql-client/0.1
Content-Type: application/sparql-query

PREFIX dc: <http://purl.org/dc/elements/1.1/>
SELECT ?book ?who
WHERE { ?book dc:creator ?who }
```

# URL-encoded POST
The query is part of a **query** "variable" (update if the operation is update) in the body of the request. The Content-Type is changed to `x-www-form-urlencoded`

```sparql
PREFIX dc: <http://purl.org/dc/elements/1.1/>
SELECT ?book ?who
WHERE { ?book dc:creator ?who }
# =>
POST /sparql/ HTTP/1.1
Host: www.example
User-agent: sparql-client/0.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 9461

query=PREFIX%20dc%3A%20%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Felements
```