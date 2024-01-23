**Definition**: Clients should not be forced to depend on interfaces they do not use.

**Example**: Interface for CRUD operations might force consumers to implement methods for all operations even if they don't want it. Instead the interface should be broken into 4 interfaces for each operation.

[[SOLID]]