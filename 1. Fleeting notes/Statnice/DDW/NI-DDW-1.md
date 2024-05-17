**Struktura a vazby na webu: principy procházení a získávání obsahu webu, grafové reprezentace - charakteristiky a využití, metriky centralit, PageRank, detekce komunit, predikce linků, afiliační sítě.**

# Crawlers
Crawlers are used to get data from the web in an automated way.
- Batch crawler - create snapshot of some web space
- Incremental crawler - continuously crawl web space, revisit to refresh data
- Focused/Topical crawler - crawl specific websites, topics

## Terminology
- Seed pages - initial pages to crawl from
- Frontier/Queue - list of unvisited URLs
- Fetcher - gets the data of a URL
- Link extractor - parses the HTML to get the links
- URL filter - check if URL is blacklisted
- Duplicate eliminator - eliminates already visited URLs
- URL prioritiser - assigns priority to URLs and sorts them by it
## Algorithms for crawling
### Breadth-first crawl
Visit pages in the order in which they are seen
It's highly correlated with their popularity, bias to index well connected sites.
### Backlink based crawl
Sort the URLs in the queue based on their relevance based on backlinks - number of links to that URL.
## Other problems
- Need to deal with bad HTML markup
- Caching and other relevant headers
- Tags for robots
- URL Normalization
	- Relative URLs should be expanded to the full form
	- Case normalization
	- Percent characters (%7E = ~)
	- Path normalization ("/a/b/../c" = "/a/c/")
	- Scheme organization (http = https)
	- ...
- Identify crawler using User-Agent header

### Robot.txt
A file that defines etiquette for crawlers to disallow robots to access certain parts of the website.

Sitemap on the other hand can inform the robot how to access the website
## Revisiting strategies
Pages get updated often -> need to revisit
- Uniform - revisit regurarly
- Proportional - revisit pages that change more often more often
- Hybrid - balance


# Scrapers
Crawlers for indexing, search engines, following links and discovering
Scrapers for obtaining information from sources without an API; they are usually more specialised to collect specific data from predefined web space.


# Grafova reprezentace
- Adjacency Matrix - all combinations of nodes (NxN matrix)
- Edge-list: list of {from: node, to: node, value: X}
	- Adjacency list: list of {from: node, edges: (Node, Value)\[\]}

## Centrality 
Trying to measure how important/popular/central a node is.

### Degree centrality
Centrality of a node = how many edges lead from + into the node.
We can also measure the in-degree centrality and out-degree centrality (only counting in/out edges)
### Closeness centrality
The mean length of all shortest paths from a node to all other nodes.
Also can be defined as inverse of farness: $C_x= \frac{1}{\sum_y d(y, x)}$ 
### Betweenness centrality
The number of shortest paths that pass through a node divided by all shortest paths
### Eigenvector centrality
1. Assign 1 to all nodes
2. Recompute scores of each node: $v_i = \sum_{j \in N} x_{i,j} \times v_j$ where $v$ is the value and $x$ is the entry in the adjacency matrix
3. Normalize $v$ values by dividing them by the maximum $v$
4. Repeat until there are no changes

Similar idea to google page rank
