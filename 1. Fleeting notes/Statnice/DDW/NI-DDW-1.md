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
## Bridges
Bridge is an edge that if removed splits the graph into 2 components

Local bridge - edge of 2 nodes that have no nodes in common. A local bridge if removed causes the distance between those two nodes to increase by more than 2.
### Neighborhood overlap
$NO = \frac{\#Neighbours\ of \ both\ A\ and\ B}{\#Nejghbours\ of\ either\ A\ or\ B}$ 
Local bridge => NO = 0
### Embeddedness 
Number of common neighbours two nodes have
## Network level characteristics
### Density
ratio between number of edges and number of possible edges
Total number of edges
- Undirected: $n \times (n-1)/2$
- Directed: $n \times (n - 1)$
### Reciprocity
Total number of reciprocated edges (edges in both directions) compared to the total number of possible edges.
## Homophily
Groups share friends among each other and are not friends with other groups.

We can test for this by calculating the probability of an edge having 2 nodes from different groups, if the probability is too low then there is homophily.
# PageRank
Idea: If a page is pointed towards by an important page, then that page is also important.
## Matrix approach
Build a hyperlink matrix that has values based on how many. Sparse matrix there are algorithms to compute fast.

There are problems:
- Rank sink (pages with no out-links can trap the rank)
- Link farms (pages pointing to each other can farm rank)
- Cycles (pages forming a cycle can cause oscillations)
## Random Surfer
Idea: have a random surfer browse the graph with an equal probability of following each link (if there is no link then teleports). The probability of the surfer being on a certain page is the rank.

**Problems to fix:**
- Convergence issues - matrix is not irreducible and not aperiodic.
- Dangling pages - pages with no outgoing links.

**Solution:** damping factor - 
- surfer chooses one of the links with probability $d$
- surfer jumps to a random page with probability $1-d$
This way the matrix becomes strongly connected (=> irreducible) + aperiodic (surfer is not following a cycle)
- Irreducible = Markov chain has a single state distribution (ensures convergence)
- Stochastic = Ensures that the result is still stochastic
- Aperiodicity = Ensures there are no oscillations
## $G = d \times S + (1-d) \frac{E}{n}$
- $G$ - Google matrix - stochastic, irreducible, aperiodic matrix, hold probabilities of moving from page i to page j with the other factors as well (teleportation).
- $d$ - damping factor
- $E = e \times e^T$ - n by n matrix of all 1
- $S$ - Matrix with links ($s_{i,j}$ is the probability of following a link from page i to page j)
- $n$ - number of pages

We can then use $G$ to compute the page rank $\pi$ iteratively:
## $\pi^{(k+1)} = \pi^{(k)} \cdot G$
- $\pi$ is a vector of n elements holding the page rank value of all pages for the $k$ and $k+1$ iteration.
- $G$ is the Google Matrix

### Improvements
- Instead of $E = e\times e^T$ we can use some $v^T$, a personalisation vector, making the result personalised.
- Modification of the $S$ matrix to be more intelligent.

# Community Detection
Community is a set of nodes that have more edges between each other compared to the number of edges leading outside the set.

## Clustering Coefficient
For each node we can calculate the clustering coefficient:
number of triads it's part of / number of neighbours
- Triad = three nodes fully connected to each other (3 edges)
- Globally this says how clustered the graph is
- Locally it says how integrated the node is (how afraid it is of interacting with others)

## Graph Partitioning

### Min-cut
Partition the graph into the components while minimising the weight lost by removing the edges.
#### Kernighan-Lin
Heuristic approach
1. Generate a random solution by randomly splitting nodes into two equal communities
2. Improve the solution:
	1. For each node compute the gain of the node being swapped to the other community
	2. Find two nodes from both communities that would be the most beneficial to be swapped
	3. Lock them to be not considered next time
3. Repeat 2 until there is no more improvement
#### Girvan-Newman
1. Start with the whole graph
2. Remove edge based on betweenness
	- Number of shortest paths through that edge
3. Recalculate all betweennesses
#### Clique Percolation Method
For overlapping communities
Idea: Inside a cluster there is a high probability of a clique connection; outside/between clusters there is lower probability

1. Find all cliques of size $k$
2. Construct a graph of cliques (1 clique = 1 node)
3. Connect these cliques if they share $k-1$ nodes.
4. Community is a component of the clique graph.
![[Pasted image 20240518152003.png]]
The clique graph now has cliques as nodes!

# Link Prediction
Is the probability of an edge forming between nodes in the future

## Supervised Learning
Using a binary classifier

## Unsupervised Learning
We calculate a Score(x, y), higher the number = higher the probability of a link forming.
### Graph Distance
Idea: Individuals are linked through short chains

Score(x, y) = -shortestPath(x, y)
### Common Neighbours
Idea: Two people have a common friend => they might get introduced to each other by that friend

Score(x, y) = $|N(x) \cap N(y)|$
Take the number of friends in common
### Jaccard's Similarity
Idea: Normalizes Common Neighbours approach; if someone has a lot of friends and they happen to share one with somebody it doesn't mean as much.

Score(x, y) = $\frac{|N(x) \cap N(y)|}{|N(x) \cup N(y)|}$
### Preferential Attachment
Idea: Nodes with higher degree have a higher chance of attracting new links

Score(x, y) = $|N(x)| \cdot |N(y)|$
### Adamic/Adar
Idea: Consider common neighbours but put more importance on neighbours that are more rare.

Score(x, y) = $\sum_{z \in N(x) \cap N(y)} 1/log|N(z)|$

## Path-based topological patterns
### Katz
Idea: The more nodes are connected through some intermediary nodes (and the shorter these paths are) the more similar the nodes are.

Score(x, y) = $\sum_l^\infty \beta^l \cdot P(x, y, l)$
- $\beta$ - (0,1) parameter
- l - length of the path
- P(x, y, l) - number of paths from x to y with length l

# Affiliation Networks
They are multimodal networks (nodes of different types), they connect some individuals with groups of individuals.

![[Pasted image 20240518161519.png]]We can use adjacency matrices PP, PT, TT (and $PT^T$) and multiply them together to learn about the network.