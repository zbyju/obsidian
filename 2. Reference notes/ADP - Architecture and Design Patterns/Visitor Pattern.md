- A behavioral design pattern that allows adding new operations to objects without modifying them.
- Involves two components: the 'Visitor' that carries the operation to be performed and the 'Element' objects that accept the visitor.
- The visitor implements different operations, and the elements offer an interface to accept visitors.

# Example
Consider a graphics application with shapes like circles, squares, and triangles. Instead of embedding rendering logic in these shapes, a `RenderVisitor` can be created. Shapes will accept this visitor, which then executes the rendering operation. This way, if a new rendering technique is introduced, only the visitor needs to be modified, not the shapes.

# Diagram
![](https://i.imgur.com/mvTJ2wS.png)


[[Behavioral Patterns]]