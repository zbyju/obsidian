# Pros
- Avoid tight coupling between the creator and the concrete products
- It makes it easier to introduce new product variants
- [[Single Responsibility Principle]] - move the product creation into one place
- [[Open-Closed Principle]] - you can make new types of products without breaking existing code
# Cons
- Code may become more complicated
# Use Cases
- When we don't know beforehand what types and dependencies of the objects are

[[Factory Method Pattern]]