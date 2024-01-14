It is the fourth principle of linked data.

Along with the provided information we should also include links to other related resources. Clients can then discover additional information.

Types of links:
- Relationship links
	- Links to related things
	- Enables retrieval of contextual information
- Identity links
	- Links to URI aliases - same resource in a different data source
	- Allows to get different opinions, or more information
- Vocabulary links
	- Links among terms in vocabularies
	- Improve data integration

```turtle 
# Relationship links
<http://biglynx.co.uk/people/dave-smith>
	rdf:type foaf:Person ;
	foaf:name "Dave Smith" ;
	foaf:based_near <http://sws.geonames.org/3333125/> ;
	foaf:based_near <http://dbpedia.org/resource/Birmingham> ;
	foaf:topic_interest <http://dbpedia.org/resource/Wildlife_photography
	foaf:knows <http://dbpedia.org/resource/David_Attenborough> .

# Identity links
<http://dbpedia.org/resource/Prague>
	owl:sameAs <http://cs.dbpedia.org/resource/Praha> .

# Vocabulary links
<http://biglynx.co.uk/vocab/sme#SmallMediumEnterprise>
	rdf:type rdfs:Class ;
	rdfs:label "Small or Medium-sized Enterprise" ;
	rdfs:subClassOf <http://dbpedia.org/ontology/Company> ;
	rdfs:subClassOf <http://umbel.org/umbel/sc/Business> .
```

[[_SWE Reference]]
[[Linked Data]]