**Definition**: Dependencies should be on abstractions - interfaces, abstract classes, not on concrete implementations. Abstractions should be made general (also avoid dependency on some low-level implementations).

**Example**: We have a UserService that wants to save Users to a DB. It should no depend on a specific class, but rather on an interface that exposes necessary functionality.

**Linkage:**
- [[_ADP Reference]]
- [[SOLID - Definition and Context]]