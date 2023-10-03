**Definition**: High-level modules should not depend on low-level modules. Both should depend on abstractions (like interfaces or abstract classes). Additionally, abstractions should not depend on details, but details should depend on abstractions.

**Example**: Instead of directly instantiating a database connection in a "UserService" class, it could depend on an "IDatabaseConnection" interface. The actual database implementation class would then implement this interface.

**Description**: DIP ensures that high-level modules remain unaffected by changes in low-level modules, promoting a structure that is more resilient to changes and easier to maintain and scale.

**Linkage:**
- [[_ADP Reference]]
- [[SOLID - Definition and Context]]