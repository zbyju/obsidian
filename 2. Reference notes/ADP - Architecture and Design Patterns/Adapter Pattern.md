- The adapter pattern is a solution to incompatible interfaces in software components.
- It enables a system to use classes that would otherwise not be compatible due to mismatched interfaces.
- It works by converting the interface of a class into another interface that the client expects.
- The adapter pattern allows the interaction without altering the original code that was not designed to work together.

Improves Principles:
- Open/Closed
- Single Responsibility

*Example: One service works with JSON, one with XML, we want them to work together, so we connect them using an adapter that converts JSON <-> XML* 

**Linkage:**
- [[_ADP Reference]]