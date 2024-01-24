Decouples the abstraction from its implementation so that the two can vary independently. It acts as a bridge between abstraction and its implementation.

# Example
Drawing shapes: we have different shapes (circles, squares, ...) different rendering methods (raster, vector). Bridge allows us to separate the shape's abstraction (the shape itself) from the implementation (how it's drawn) so that these things can be changed independently.

# What Problem it Solves
- Prevents cartesian product complexity explosion
- Enables changing abstraction and implementation independently

# Diagram
![](https://i.imgur.com/QUY0P9i.png)
1. Abstraction provides high level logic
2. Implementation declares the interface that's common for concrete implementations
3. Concrete implementations contains specific code
4. Optionally Refined Abstractions provide variants of the logic. They work with the implementations through the implementation interface
5. Client is usually only interested in working with the abstraction.
