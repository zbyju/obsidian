SPARQL also specifies how the results are going to be returned, which is dependent to the type of query. The results are usually shown in a tabular format to the a human user, but for a machine they can be returned in various different formats.

# SELECT

Results can be returned as JSON, XML, CSV or other.

# ASK

Result is a single boolean and can be returned inside JSON.

# CONSTRUCT, DESCRIBE

They return a whole graph, therefore they need to use some RDF format: RDF/XML, Turtle, N-triples, JSON-LD, etc.

[[_SWE Reference]]
[[2. Reference notes/SWE - Semantic Web/SPARQL|SPARQL]]