# Pros
- [[Single Responsibility Principle]] - you can decouple classes that invoke operations from classes that perform them
- [[Open-Closed Principle]] - You can introduce new handlers into the app without breaking existing client code
# Cons
- Some request can end up unhandled
# Use Cases
- When we need to pass an object through a chain of some checks/handlers/middlewares.
- When we need loosely-coupled decision making.

[[Chain of Responsibility Pattern]]