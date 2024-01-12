B Trees' structure and usage in databases.
- It's a balanced tree (B Tree) with leaves connected as bidirectional linked lists.
	- These linked lists are for operations like <, >, <=, >=.
	- Therefore, it's not a pure B Tree but usually called B* Tree or B+ Tree.
- In practice, the tree's depth is typically max 4 because of its wide nature.
- Access cost through an index is the tree depth + 1.
- The inner entries don't hold data entries - only leaves do.

[[_PDB Reference]]
[[2. Reference notes/PDB - Advanced Databases/B Tree|B Tree]]
[[Access Methods in Databases]]
[[Heap table with index]]