- Wraps an object to provide new behaviors or responsibilities without changing its interface.
- Allows for dynamic addition of functionalities to individual objects without affecting the behavior of other objects from the same class.

Improves Principles:
- Open/Closed
- Single Responsibility

*Example: A data stream object can be decorated with compression and encryption functionalities. Adding `CompressionDecorator` and `EncryptionDecorator` enhances the basic stream without altering its core functionality and allows for flexibility in configuring the stream's capabilities.* 

**Linkage:**
- [[_ADP Reference]]