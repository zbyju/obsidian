- Manages a hierarchical tree structure by treating individual objects and compositions of objects uniformly.
- Facilitates client code that treats single objects and compositions similarly, simplifying the client interface.

Improves Principles:
- Open/Closed
- Single Responsibility

*Example: In a graphics application, both single elements (like shapes) and groups of elements can be treated as `Graphic` objects. Whether it's a single `Line` or a composite `Picture` consisting of many shapes, the `draw` method can be called on any `Graphic`, simplifying the client code.* 
