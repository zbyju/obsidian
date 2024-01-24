(also known as Wrapper)

- The adapter pattern is a solution to incompatible interfaces in software components.
- It enables a system to use classes that would otherwise not be compatible due to mismatched interfaces.
- It works by converting the interface of a class into another interface that the client expects.
- The adapter pattern allows the interaction without altering the original code that was not designed to work together.

# Example
One service works with JSON, one with XML, we want them to work together, so we connect them using an adapter that converts JSON <-> XML

# Diagram
![](https://i.imgur.com/UKj6aqw.png)
1. Client is some class that is already implemented and contains business logic
2. Client interface describes a protocol that other classes must follow to collaborate with it
3. Service is some class the client can't communicate with
4. Adapter is a class that