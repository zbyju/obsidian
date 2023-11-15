- Optimizes memory usage by sharing common parts of state between multiple objects instead of keeping all data in each object.
- Useful in scenarios where a large number of similar objects are used, offering significant memory savings.

Improves Principles:
- Open/Closed
- Single Responsibility

*Example: - In a shooting game, bullets can be numerous and share common properties like texture, speed, and size. These shared attributes are stored in a single flyweight object. Each bullet instance then holds only its unique state, like position and trajectory, referring to the shared flyweight object for common properties, significantly reducing memory usage.*

**Linkage:**
- [[_ADP Reference]]