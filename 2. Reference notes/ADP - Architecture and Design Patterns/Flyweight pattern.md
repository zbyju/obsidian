- Optimizes memory usage by sharing common parts of state between multiple objects instead of keeping all data in each object.
- Useful in scenarios where a large number of similar objects are used, offering significant memory savings.

# Example
In a shooting game, bullets can be numerous and share common properties like texture, speed, and size. These shared attributes are stored in a single flyweight object. Each bullet instance then holds only its unique state, like position and trajectory, referring to the shared flyweight object for common properties, significantly reducing memory usage.

# Diagram
![](https://i.imgur.com/c068WgA.png)
1. Flyweight is an optimization - debug the performance and find out if there is a RAM problem, then implement it.
2. Flyweight contains a portion of the original object's state that can be shared across multiple objects.
3. Context contains the extrinsic state (unique across objects). If it paired with the flyweight that holds the intrinsic state (common across objects), it represents the full state.
4. Usually the implementation is in the flyweight object, we then have to pass the data that it needs to run the operations.
5. Client stores the extrinsic state in context

[[Structural Patterns]]