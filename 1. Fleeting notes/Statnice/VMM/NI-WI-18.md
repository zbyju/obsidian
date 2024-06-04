**Metrické indexování, principy a metody. Techniky pro aproximativní vyhledávání.**
# Metric Access Methods
=> faster index in databases using metric index:
- lower-bounding using pivots
- similarity function needs to be metric

## Problems
Calculating distances is expensive
### Lower bounding
general mechanism for making it more efficient
using cheap lower bound instead of expensive distance

Lower bounding can be done in metric model using pivots.

Lower bound helps as it splits the space so that we can focus only certain part.
### Pivots
constant number of pivots based on which we index

We have a query Q, pivot P and object X. The distance can be calculated as Q->P->X where Q->P can be calculated only constant number of times and P->X is stored in the database. The overall distance D <= Q->P->X.

We can then rule out X, or even a cluster of Xs that are close to P or based on a partition of the space.
#### Partitioning
![[Pasted image 20240529000451.png]]
- Pivots create a partition of objects that are closest to them.
- Query is placed somewhere in the space
- If the smallest distance from a pivot to the query region (Oi to Q) is bigger than the furthest distance from another pivot to the region (Oj to Q) then we know that no objects from Oi partition can be inside Q.
#### Number of pivots
They are good if they are close to data or close to query, therefore we choose pivots:
- Based on data
- Based on queries (e.g. previous queries)

- Choose quality pivots
- Choose quantity (statistically gonna work)
- Choose both
### Choosing pivots
#### Random
Good when we choose a lot
#### Random groups
Choose several groups at random and then choose the best group
Best group = distances between them are high
#### Incremental
1. Choose random
2. From a random group choose another pivot that maximizes the mean distance
#### Sparse Spatial Selection
Calculates optimal number of pivots
Use incremental until the mean distance of pivots is higher than some threshold
### Curse of Dimensionality
In higher dimensions the objects are suddenly far away from each other. There is too much space where they can be. Low chance for clusters.
## Pivot tables
Matrix method:
- each object O maps to a vector o
- => distance matrix

We want to avoid sequential L2 distances as much as possible (and want to use Linf distance in pivot space)

Left is the vector space; right is the pivot space based on pivots P1, P2 (number of pivots determine the dimension of pivot space - 2 pivots = 2D pivot space). ![[Pasted image 20240525215551.png]]
### AESA
- Every data object is a pivot => square matrix O(|S|^2)
- Distance between all objects
- O(1) time for finding nearest neighbor space
- Expensive construction
### LAESA
- Only using k data objects as pivots O(|S|\*k)
- We can use $L_{\infty}$ metric in pivot space (square ball)
	- = max distance in either vertical or horizontal direction
	- This is only approximate distance to the previous one
		- It's contractive (distance is either same or smaller; never bigger)
	- we get some candidates that we need to verify in the original vector space
- It is faster because we use square distance and not circle
#### Range Query
1. Find candidates using square
2. Refine the result by calculating distances using L2 for candidates
#### Nearest neighbor
0. Have the precomputed distances between each point and all the pivots
1. Initialize minimum distance to infinity; consider all pivots, query Q
2. Select random pivot
	- Compute L2 distance Q-P (each pivot represents some coordinate of the query vector)
	- if new distance is lower than min distance then update min distance and candidate to closest neighbor.
	- remove pivot from set of points
3. Elimination
	- Filter all those objects for which the Linf distance is bigger than min distance (lower bound)
4. Approximation
	- If set of points is empty then we found nearest neighbor
	- Othewise continue with pivot which has lowest Linf to the query and is still in the set
### Improvements
Representing in a better way than in matrix (R-Tree)
## Tree-based index
### GH-tree
Binary tree based on pivots
1. select two pivots
2. partition the database into two groups
3. recursively repeat for the two partitions

Static

When making a range query we test overlap of both partitions and if the query only effects one partition we can filter out the other one
Here the query effects both partitions (pivots are Q1 and Q6): ![[Pasted image 20240525225021.png]]

### GNAT
Generalized GH-tree with n pivots (not just 2) 
Static

We can again filter out partitions if some partition is more distant than the furthest possible object inside the query![[Pasted image 20240525225333.png]]

### VP-tree
1 pivot + n radius numbers
Static

![[Pasted image 20240525225714.png]]

### MVP-tree
n pivots, n\*m radius numbers
### M-Tree
Inspired R-tree (similar to B-tree)

B-tree but instead of intervals we have balls (L2)

Dynamic and can grow as the database evolves (inserts, deletes)
### PM-Tree
There is a lot of dead space (big area, low amount of points)

M-Tree + trying to reduce all the balls using some rings such that it still contains all the points

![[Pasted image 20240525230444.png]]

## Hash-based index
### D-Index
Uses ball-partitioning split functions hashing which is locally sensitive (close objects have similar hash)

Create 3 regions based on pivot (e.g. O12) and assign value for each object based on where it is:
- In = 0
- Ring = 2
- Outside = 1

![[Pasted image 20240525233915.png]]

Then we concat these values from different pivots to get the final value as a "binary" value:
- If there are only 0 and 1 in the output then it's fine
- If there is some 2 in the output (the point was in the ring) then we deal with it separately
	- Partition the set of rings again and index the problematic points again
	- Do this until there are no problematic points left or the partition is very small

We can choose d - radius of region, $\rho$ - radius (half width) of the ring
- Bigger $\rho$ -> less performance we are going to get (a lot of elements inside rings)
- Lower $\rho$ -> efficient query only when query radius < $\rho$ so it limits queries.
=> good for queries that have small radius
- Finding almost duplicit elements
## Index-free MAM
### D-File
original database with sequential scan + cache
All online, nothing pre-calculated, build the cache from previous queries
D-cache:
- caches distances (not distances themselves) for easy calculation of lower bounds
Similar to LAESA but instead of pivots we consider previous queries and then we use previously calculated values for faster computation
# Approximate Similarity Search
https://www.youtube.com/watch?v=jaXrY5faZJU&list=PLVNPGcDPZ_tsuMxLBeiQlvn0z23Tv4zGM&index=16
Exact search might be too slow, so we trade precision for performance
- Even metric axioms don't result in quick enough indexing/search
- Trade precision for faster queries
- This is beneficial if data is hard to index
	- = hard to cluster/group them
- Similarity functions don't mimic human similarities

Strategies:
- guarantee of a bound
	- every object in the result is somehow relevant
- probabilistic
	- every object in the result is relevant with some probability
- no guarantees
## Intrinsic Dimensionality
value showing how indexable a dataset is
$\rho(S, d) = \mu^2 / 2\sigma^2$ (S - dataset, d - distance function, mean and variance)

![[Pasted image 20240528231119.png]]

Low value = easy to index because distances are variable
High value = hard to index because objects are almost equally distant (no clusters)

# Techniques
## Pivot tables
We can use LAESA and skip refinement step.
We need enough pivots and then it can work.
## FastMap
Metric space is in fact Euclidean space (of user defined dimensionality)

It recreates the coordinates from pairs of pivots (each pair = pivot axis).
0. Let's construct euclidean space of dim k 
1. select best pivot pair
	1. select object at random
	2. select 2 objects that are furthest from that object
	3. those are the pivots
## M-tree
Metric index which uses kNN for exact indexing.

We can improve this:
- Terminate early if the array of nearest neighbors changes only a little
- If the distance to the kth element is low enough then terminate
- Use PAC queries (Probably Approximately Correct)
## Permutation Indexes
Consider a set of k pivots and pivot table
instead of a distance matrix we store pivots as ordered collection (closest to furthest)

e.g.: 
```
Object o1: p1, p4, p2, p3
Object o2: p2, p1, p4, p3 
```
We then use permutation distance on this space (how similar are the permutations)

Distance: $D(u, q) = \sum_{1 \le i \le k} (P_u(i) - P_q(i))^2$ (P - position in the permutation of object)
