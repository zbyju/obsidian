(also know as Wrapper)

- Wraps an object to provide new behaviors or responsibilities without changing its interface.
- Allows for dynamic addition of functionalities to individual objects without affecting the behavior of other objects from the same class.

A data stream object can be decorated with compression and encryption functionalities. Adding `CompressionDecorator` and `EncryptionDecorator` enhances the basic stream without altering its core functionality and allows for flexibility in configuring the stream's capabilities.

# Diagram

![](https://i.imgur.com/lHeq7py.png)
1. Component declares a common interface for wrapped objects and wrappers
2. Concrete component is the class that gets wrapped. It then can get enhanced by decorators.
3. Base decorator
