**Textové a bag-of-words modely pro vyhledávání podle obsahu. Podobnostní model vyhledávání, podobnostní míry a dotazy.**

# Text based model
Useful for other media retrieval too (images, videos, sounds, ...) if we have a text description of those media files.

Terminology:
- Collection = set of all documents ($d_j$ - document with index j; there are n documents)
	- Matrix = rows have documents; columns have terms
- Vocabulary = set of all terms in collection ($t_i$ - term with index i; there are m terms (usually 10,000-100,000))
- Document = some text (usually 100-1000 terms)
	- Unordered set of terms ($d_j = \{t_{i1}, t_{i2}, t_{i3}, ..., t_{ik}\}$ )
- Query = query document or set of keywords (usually 10)

- Input = any text
- Preprocessing:
	- Remove unwanted characters (HTML tags, punctuation, numbers, ...)
	- Break into words
	- Simplify terms (lematization, stemming)
	- Remove stop words
	- => Index Terms (result)
## Boolean Model
document = $d_j = \{0|1, 0|1, 0|1, ..., 0|1\}$
Each document is represented by the terms it includes (we don't count them just 0/1)
Can be represented as a set (of all terms) or a vector (very sparse; 1 only where the term is in the document).

We can use boolean expressions for queries. The result is a set of documents that are true; no ranking; no partial match. It is similar to SQL queries.

- Simple
- Easy to understand
- Limited expressive power
- No ranking
- Hard to control the number of documents retrieved
- Hard to improve the query
- Document is very different from the query (document = vector; query = boolean expression) - hard to create query from document
### Inverted Index
Instead of having a list of terms for each document, we have a list of documents for each term. 

This is better because it deals with sparsity => less memory needed for representation.
When evaluating a query we only look at very limited part of the index => faster evaluation.
## Vector Model (Bag of Terms; Bag of Words)
bag = multi-set = set allowing multiple occurrences of the same element
Same input as boolean model but instead of 0/1 we have occurrence count.

document = $d_j = \{c_1, c_2, c_3, ..., c_k\}$
query is made of keywords with optional weights:
$q = \{t_1(0.5), t_6(0.8), t_{29}(0.2)\}$ (each term has weights between 0 and 1)
matrix
### Occurrences (weights)
$f_{ij}$ - frequency of term i in document j
$tf_{ij}$ - normalized frequency ($= f_{ij}\ /\ MAX_j f_{ij}$)
- How important the term is within one document
$df_i$ - document frequency of term i (number of documents that have term i)
$idf_i$ - inverse document frequency of term i ($= log_2 (n\ /\ df_i$)
- How universal the term is (useless for queries)
- Log is because we don't want to have a linear curve; we want to filter out the common words but not boost unique terms too much
##### TF-IDF
$w_{ij} = tf_{ij} \times idf_i$

High weight = unique term within collection but high occurrence in document
##### Consine Similarity
$CS(d, q)= \frac{d \cdot q}{|d| |q|}$ (scalar product / lengths)
### Inverted Index
We can again use inverted index = each term has a list of documents + its weight within that document
### LSI (Latent Semantic Indexing)
We get a decomposition of our matrix
$A = U \Sigma V^T$ and use the $\Sigma V^T$ which is a dense matrix that has concepts instead of terms
- Deals with synonyms; hononyms
The problem is that we can't use inverted index (because matrix is dense) => not used for large scale
# Bag of Features
(bag of visual words)

If we don't have annotations we can split the image into "features" and then use those features the same we did with textual approach.
1. Extract features from images
2. Learn visual vocabulary
	- Define the space where we are going to be working
3. Quantize features
	- Create partitions/clusters of features
4. Represent images (or incoming queries) by histograms
	- Histogram = how much of each feature does that image contain (based on how many features extracted are part of each partition/cluster)
	- Each features = term; histogram = weights of features
## Feature extraction
- make a grid (very simple)
- create SIFT (interest points)
- random sampling
- segmentation
## Visual Vocabulary
1. Get features
2. Cluster them
3. Create partitions/centroids/representative features

This reduces the dimentionality

![[Pasted image 20240524142435.png]]

# Word2Vec
1. Represent each word as a vector
	- We have a vocabulary V; each word is represented as 0 at each position with 1 on position for that word

Then we have a word and its context:
The cute cat jumps over ... (cat = center word, The cute jumps over = context)

- Then we either predict the center word from the context
- Or we predict the context from the center word
# Similarity
Score of similarity = higher -> more similar
Distance = dissimilarity

Similarity = function that takes two features from feature universe and returns a real number $\delta: U \times U \rightarrow R$

## Features
We need descriptive features, but compact representation
- Vector space + distance
- Metric space model (doesn't matter what we choose but the whole thing needs to form a metric space)
- General (no characteristics for database optimizations)

- Single complex descriptor
- Multiple descriptors
### Feature extraction
We get some vectors
- Correlated dimension
	- Histogram
		- 0 is similar to 1, but very different from 255 (0 = black, 1 = almost black, 255 = white)
		- If we randomly mixed the histogram than it would be independent
- Independent dimensions
	- Concatenation of independent features
- Combined
	- Multiple histograms (RGB)
- Time series
- String, Sequence
- Set
- Geometry
- Graph
## Properties of Similarity
- Retrieval-specific
	- learning, adaptation, evolution (these are specific to the domain and implementation)
- Topological
	- Metric axioms
	- Non-metric
- Cost
	- Computational cost
	- O(n) - O(2^n)
### Metric Similarity
- Reflexivity
	- Object is maximally similar to itself
	- Only the same object has distance = 0
- Non-negativity
	- Two very distinct objects are somehow dissimilar
- Symmetry
	- Direction of similarity is not important
- Triangle inequality
	- Similarity is transitive

Non-metric similarity:
- More simple
- Sometimes more intuitive
- Robust
	- Ignoring noise
- Blackbox similarity (we can't verify)
- But we lack the axioms to work with
	- Harder to index
	- => O(n) find
## Smart Descriptors vs Smart Similarity
We can have:
- Smart descriptors and simple similarity
	- Feature extraction does most of the logic
	- Better
	- Harder to create descriptors
	- Easier to interact with user
		- User can use natural language
	- Cheaper similarity
		- O(n)
- Simple descriptors and Smart similarity
	- Only when we can't make smart descriptors
	- We need to match different types of data if we have natural language query
	- Semantic gap
	- Sometimes necessary
	- Smart similarity is costly
		- O(n^2) and worse
## Similarity Queries
### Range Query
For a query Q we create a query radius $r_Q$ and return all objects that are close enough.

![[Pasted image 20240524161708.png]]

The user needs to choose the $r_Q$ radius, which can be a problem.
=> 100% recall
### K-Nearest Neighbors (kNN)
Q Query and number k of most similar objects.

Very similar to range query where the range is the distance between the k-th closest element to the query (we could find that distance after evaluating the query).

- More user friendly
- Recall is harder to achieve
- Can be solved by pagination

1. Start with radius = infinity
2. Count how many results we have
3. Choose random sample of k elements
4. Use the furthest elements as new radius
5. Repeat until we have k elements
### Reverse kNN
Q Query and number k
Return all objects that have Q as in their set of k nearest neighbors

Can be used for finding the density of the place of Q
### Reranking
Multiple query stages that make the result set smaller with each step.
## Similarity Functions for Vectors
## Lp Distance
$L_p(v,u) = (\sum_{i=1}^{D} |v_i - u_i|^p)^{1/p}$

![[Pasted image 20240524164516.png]]
## Cosine Similarity
Non-metric (only symmetry)

We can make it pseudometric by using arccos to get the angle.
## Fractional Lp Distance
use p < 1
non-metric
robust - noise is less counted (noise is square rooted)
## Weighted Lp Distance 
$L_p(v,u) = (\sum_{i=1}^{D} (w_i \cdot |v_i - u_i|)^p)^{1/p}$

Puts more emphasis on some dimension.
Makes the space into ellipsis
## Kullback-Leibler divergence
non-metric
Measure how inefficient it is to code one histogram as another.
## Jeffrey Divergence
non-metric

Similar to Kullback-Leibler (but with symmetry)
## $\chi^2$ distance
non-metric

Measure if two distributions were produced from the same underlying distribution
## Quadratic form distance
Correlated dimensions supposed
We do a euclidean distance + we multiply with correlation matrix
Can make it more robust by also weighing in how close the dimensions are close to each other
## Earth Mover's Distance
metric

Minimal amount of work to turn one pile X into pile Y
We take into consideration:
- f - how much mass needs to be moved
- c - how costly is it to move from pile i to pile j
	- moving from piles close to each other is less costly

$O(D^3 log D)$ when both histograms are of equal dimensionality
$O(2^D)$ otherwise
## Composed
- Linear combination of metrics => still metric
- Multiplication of metrics => non-metric
- Any combination with non-metric => non-metric
## Neural Network
Let neural network to find out the similarity formula on its own
## Similarity Functions for Sequences
(time-series)
## L2
We can treat the sequence as a vector and then use any vector similarity such as L2.
## Dynamic Time Warping Distance (DTW)
non-metric
- Allows stretching one series (even just locally) to match the other
- Sequence alignment

We try to align it such that:
- we start at the beginning of each sequence
- we can't reorder the sequence
- we can't go back in time

We then use the path that minimizes the distance.

We can introduce more constraints to improve and avoid bad alignments by trying to stick close to the initial alignment and only reordering slightly:
![[Pasted image 20240524172057.png]]

This improves computation time as well by only considering solutions in some subregion.
## Similarity Functions for Strings
## Edit Distance
O(mn) Dynamic programming
metric

How many operations do i need to make to turn string A into string B by using insert, delete, replace
## Hamming Distance
O(n) metric

Edit distance with only substitution (=how many letters match)
## Longest Common Subsequence
non-metric
O(mn)

Subsequence is not substring

Measures how many letters are in the longest subsequence
# Similarity Functions for Sets
## Jaccard Similarity
$\frac{A \cap B}{A \cup B}$
## Hausdorff Distance
Measuring the furthest nearest neighbor
1. Consider all elements a in A
2. Find nearest neighbor b for a
3. Return the distance between a, b that was the highest
4. Do the same with all elements of B
5. Return the overall maximum

Good for when we need to be confident - we are taking the furthest points 
