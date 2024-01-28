# Pros
- [[Open-Closed Principle]] - you can introduce new behavior without changing existing code
- [[Single Responsibility Principle]] - same behavior in the same class
- Visitor can be easily used with some complex data structures by simply calling the `visit` method without inspecting what class it is.

# Cons
- You need to update all visitors when adding/removing a new class to the hierarchy 
- Visitors might lack access to private fields

# Use Cases
- When working with hierarchies
- When separating algorithm from objects they operate on

[[Visitor Pattern]]