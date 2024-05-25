**Metrické indexování, principy a metody. Techniky pro aproximativní vyhledávání.**

# Metric Access Methods
=> faster index in databases using metric index:
- lower-bounding using pivots
- similarity function needs to be metric
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