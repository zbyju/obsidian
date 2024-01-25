Lets you traverse a collection without exposing the underlying representation.

# Example
In a custom data structure, such as a complex linked list or a tree, an iterator can be implemented to provide a standardized way of traversing the structure. The client code can then use this iterator to access elements sequentially without needing to understand the internal structure of the collection.

# Diagram
![](https://i.imgur.com/cmbqn56.png)
1. Iterator interface declares a method to get the next element and then method for checking if there is a next element.
2. Concrete Iterator implements specific algorithms for iterating over a specific collection. It should be able to traverse it on its own and hold the state - this allows us to have multiple iterators over the same collection.
3. Collection interface declares methods of obtaining an iterator.
4. Concrete collections return new instances of a concrete iterator each time client requests one. This is the class that implements all the methods and functionality of the collection
5. Client works with both the collections and the iterators. They request collections to give them iterators.

[[Behavioral Patterns]]