- The Bridge pattern separates an object’s interface from the actual implementation (the code that does the work), allowing them to be varied independently.
- It improves flexibility and readability by decoupling code, leading to a system that’s easier to reconfigure and scale.
- This pattern is beneficial when you need to extend a class in multiple orthogonal (independent) dimensions.

Improves Principles:
- Open/Closed
- Single Responsibility

*Example: One service works with JSON, one with XML, we want them to work together, so we connect them using an adapter that converts JSON <-> XML* 