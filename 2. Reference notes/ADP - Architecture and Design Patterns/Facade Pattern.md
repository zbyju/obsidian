- Provides a simplified interface to a complex subsystem or set of interfaces, making the subsystem easier to use.
- Coordinates the system's underlying complexity by exposing a unified higher-level interface to the client.

Improves Principles:
- Single Responsibility

# Example
Smart Home: a `HomeAutomationFacade` can provide a simplified interface to control the smart home. Rather than interacting with each system separately, a user can use the facade to execute common routines like "Leaving Home" or "Movie Night," which internally manages the complex interactions between different subsystems.

# Diagram
![](https://i.imgur.com/RTWZXNR.png)
1. Facade provides convenient access to some subsystem. It combines multiple other classes to provide some funcitonality
2. Additional Facade can be created to prevent from polluting the original Facade with unrelated features. Additional facades can be used by both clients and other facades.
3. Complex subsystem consists of many objects. These objects are not aware of the facade; the facade uses them for complex operations
4. Client uses facades instead of calling many different objects

[[Structural Patterns]]