- Provides a simplified interface to a complex subsystem or set of interfaces, making the subsystem easier to use.
- Coordinates the system's underlying complexity by exposing a unified higher-level interface to the client.

Improves Principles:
- Single Responsibility

*Example: Smart Home: a `HomeAutomationFacade` can provide a simplified interface to control the smart home. Rather than interacting with each system separately, a user can use the facade to execute common routines like "Leaving Home" or "Movie Night," which internally manages the complex interactions between different subsystems.*

# Diagram
![](https://i.imgur.com/RTWZXNR.png)
1. Facade provides convenient access to a set of 

[[Structural Patterns]]