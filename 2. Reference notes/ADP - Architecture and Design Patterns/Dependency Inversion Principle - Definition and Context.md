**Definition**: Dependencies should be on abstractions - interfaces, abstract classes, not on concrete implementations. Abstractions should be made general (also avoid dependency on some low-level implementations).

**Example**: We have a UserService that wants to save Users to a DB. It should no depend on a specific class, but rather on an interface that exposes necessary functionality.

Instead of directly instantiating a database connection in a "UserService" class, it could depend on an "IDatabaseConnection" interface. The actual database implementation class would then implement this interface.

**Description**: DIP ensures that high-level modules remain unaffected by changes in low-level modules, promoting a structure that is more resilient to changes and easier to maintain and scale.

**Linkage:**
- [[_ADP Reference]]
- [[SOLID - Definition and Context]]