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
Problems: The other application must understand the complex structures and contraints of the data
Good for bulk data

## Service-oriented
Integration on application level
Hide implementation details, expose interfaces
Problems: can become hard to manage if not properly designed
Good for real-time data

SOA provides both service oriented and data oriented approaches

### ESB
Provides:
- Message broker
- Location transparency
- Dynamic routing
- Mediator for data transformations
- Session pooling
- Message enrichment

# Communication
## Synchronous
Request is sent, client waits for response.
1 socket for the whole communication

$t_{req} - t_{res}$ musi byt maly - sekundy

easy to implement
simple
only the client needs to know the location of the server
## Asynchronous
Request is sent, server sends ACK
Later Response is sent, client sends ACK
1 socket for request, 1 socket for response

$t_{req} - t_{res}$ muze byt velmi dlouhy - hodiny, dny

slozitejsi, oba musi vedet kam poslat request/response
problem s private/public sitemi

## Intermediary
Component that decouples client and server
Zlepsuje reliability - server nemusi byt available kdyz client posle request
Zlepsuje performance - muze existovat vice serveru
MQ - queue-based communication
PS - publish subcribe - event driven communication

# I/O
## Blocking (Synchronous) IO
### Inbound connections
New thread for each connection
1K connections = 1K threads = big overhead
### Outbound connection
Thread is blocked when connection is made
when connection is slow, scalability is poor

## Non-Blocking (Asynchronous) IO
### Inbound
Connection is maintained by the OS (not the app)
App registers events, OS triggers events when they occur
There might be threads if the app creates them
### Outbound
