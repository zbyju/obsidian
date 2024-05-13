**Integrační návrhové vzory, synchronní a asynchronní komunikace, blokující a neblokující I/O.**

# Integration Design Patterns
## One-to-One
Direct communication between services
Difficult to have multiple services (more than 2) communicating between each other
Leads to scalability issues as the codebase grows
Leads to tight coupling
Problems with many different interfaces/technologies/vendor lock

## Many-to-Many using ESB
Also known as the SOA architecture
Contains various integration components - process server, mediators, messaging middleware, identity management
ESB provides a lot of functionality
Spaghetti inside the ESB

## Data-oriented
Application integrates with another one through its database
In the past: monolithic; two tier client/server architectures
Today: ETL (Extract, Transform, Load)
Problems: 