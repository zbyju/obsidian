Lets you compose objects into tree structures and then lets you work with these structures as if they were individual objects.

Improves Principles:
- Open/Closed
- Single Responsibility

# Example
In a graphics application, both single elements (like shapes) and groups of elements can be treated as `Graphic` objects. Whether it's a single `Line` or a composite `Picture` consisting of many shapes, the `draw` method can be called on any `Graphic`, simplifying the client code.

# What Problem it Solves

# Diagram
![](https://i.imgur.com/bn586EN.png)
1. Component interface describes operations that are in common for the simple objects and also complex tree structures
2. Leaf are basic elements that make the tree
3. Composite it has leaves and other containers. When getting a request it delegates it to the sub-elements and then aggregates the results
4. Client works with simple and complex elements, it can do it same way without changing its behavior.