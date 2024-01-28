Lets you separate algorithms from the objects on which they operate.

# Example
Consider a graphics application with shapes like circles, squares, and triangles. Instead of embedding rendering logic in these shapes, a `RenderVisitor` can be created. Shapes will accept this visitor, which then executes the rendering operation. This way, if a new rendering technique is introduced, only the visitor needs to be modified, not the shapes.

# Diagram
![](https://i.imgur.com/mvTJ2wS.png)
1. Visitor interface declares a set of visiting methods (these methods may have the same name if the language supports parameter overloading). It gets objects through the argument to then use to implement the algorithm.
2. Concrete visitors implement different behaviors by taking the object as argument and then using it.
3. Element interface has `accept` method for accepting visitors.
4. Concrete Elements override `accept` method by passing themselves to the visitor in the `visit` method.
5. Client usually represents a collection or some other complex structure of elements.

[[Behavioral Patterns]]