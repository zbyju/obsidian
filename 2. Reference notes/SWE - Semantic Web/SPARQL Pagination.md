When dealing with large datasets we need a way to get just a fraction of the results and then either proceed to get more or stop at some number - using pagination.

It is a common pattern to use:
- ORDER BY
- LIMIT
- OFFSET
together so they provide a reliable pagination by sorting the results and then taking *x* results and paginating using the *offset*.

[[_SWE Reference]]
[[SPARQL Select Query]]
[[SPARQL Query Modifiers]]