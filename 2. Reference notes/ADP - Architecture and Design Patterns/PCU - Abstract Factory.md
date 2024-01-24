# Pros
- Enforces that products that are produced are compatible between each other
- Avoid tight coupling between concrete products and client code
- [[Single Responsibility Principle]] - product creation is extracted into a separate place
- [[Open-Closed Principle]] - introducing new variants don't break previous code

# Cons
- Code might get more complicated due to new interfaces and abstract classes.

# Use Cases
- When we need to work with various families of related products
	- but we don't want it to depend on a concrete class of those products
	- we don't know beforehand which type of product
	- we want to support all types
- Providing a library of products without exposing the implementation

[[Abstract Factory Pattern]]