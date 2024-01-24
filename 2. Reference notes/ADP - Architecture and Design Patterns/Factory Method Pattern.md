(also known as Virtual Constructor)

Provides interface for creating objects in a superclass but allows subclasses to alter the type of objects created.

# Example
We have a `Logistics` class that creates transport objects. The type of the transport object is determined by subclasses - either `Truck` or `Ship`.

# What Problem it Solves
- Decouples creation of objects from their use
- 