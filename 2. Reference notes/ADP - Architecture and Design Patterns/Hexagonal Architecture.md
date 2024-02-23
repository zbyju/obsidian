Aimed at creating loosely coupled application components that can be connected to their software environment using ports and adapters.

This leads to exchangeable components => better testing.


# Inside 
## Domain
The business logic of the app. It's independent of any knowledge about external systems (database, UI, APIs)
## Ports
They represent boundaries or interfaces through which the app communicates with the rest of the world.
# Outside
## Adapters
They adapt the external world to the application and vice versa. They mostly do data conversions/transformations.
### Primary/Driving Adapters
Trigger interactions with the domain (UI, REST API)
### Secondary/Driven Adapters
Respond to domain requests (Database, Message systems)

# Pros
- Flexibility
- Testability
- Maintainability
# Cons
- Complexity
- Learning curve
- Overhead

[[Architectures]]