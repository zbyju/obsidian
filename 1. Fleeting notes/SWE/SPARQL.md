query language
it defines the language spefication but also:
- the way the data is stored
- way of accessing the data
- formats of the output

different query forms:
- SELECT
	- define pattern and get variables that match the pattern
	- SELECT variables in output FROM data source WHERE { triple patterns to be matched }
- CONSTRUCT
	- constructing new rdf graphs (triples)
	- CONSTRUCT { output pattern } { input pattern }
	- mapping some graph to another
- ASK
	- similar to select, but return boolean value instead
- DESCRIBE
	- retrieve information about resources

we can describe the prefixes we are gonna be using (using the keyword PREFIX)
we can use a BASE prefix also (empty prefix that's gonna be used if no other prefix is used)