- The Bridge pattern separates an object’s interface from the actual implementation (the code that does the work), allowing them to be varied independently.
- It improves flexibility and readability by decoupling code, leading to a system that’s easier to reconfigure and scale.
- This pattern is beneficial when you need to extend a class in multiple orthogonal (independent) dimensions.

Improves Principles:
- Open/Closed
- Single Responsibility

*Example: Remote control interface and its interaction with devices. The `RemoteControl` class serves as the abstraction, while `Device` is the implementation that can be extended to `TV`, `Radio`, etc., without changing the remote's code.* 

**Linkage:**
- [[_ADP Reference]]