**Architektura softwarového systému, pojem služba a její charakteristiky. Architektura REST (vlastnosti, zdroj, srovnání se SOAP). Optimalizace protokolu HTTP (latence, keep-alive, pipelining)**

# Architecture
It is the structure and behaviour of the system and its parts.

There are different views on architecture (dimensions):
- Enterprise - pohled na celou organizace ktera zastresuje vsechno
	- Rozdeluje system do bloku (aplikaci); aplikace koresponduji s ruznymi domenamy (sales, finance, …):
		- OMS (Order Management System)
		- CRM (Customer Relation Service)
		- Billing and Revenue Management (BRM)
	- Rozdeluje business podle urovni:
		- OSS (Operational Support Systems)
		- BSS (Business Support Systems)
		- EIS (Executive Information System)
		- OIS (Office Information System)
		- Integration
			- B2B (Business-to-business)
			- EAI (Enterprise Application Integration)
	- Pohled na typ spolecnosti:
		- Customer (user needs, business requirements)
		- Supplier (enterprise system/application provider; solutions and customizations according to requirements)
		- Vendor (technology provider, development based on market needs)
- Data - Pohled na data, model, bezpecnost
	- For service: data model definition, input output, representation of resources
- Functional - Funkce, requirements, sluzby
	- For service: operation definition, input, output used by the operations
- Process - Pohled na business procesy, automace, monitoring
	- For service: how to use the service and its functionality
- (Technical)
	- For service: Details - security, SLA, IP, port, protocol
- Software - Pohled na architekturu ze software, vyber technologii
	- Centralized - Client/Server
		- Single point of failure
			- there is a need for a highly reliable server-side solutions
	- Decentralized - P2P
		- other nodes take function of a failing node
		- nodes can share the load
	- Usually we use centralized with p2p principles
	- Interface
		- Can be achieved using standards, social agreement or dominant position on the market
		- Data - defines communication language
		- Functions - defines entry points
		- Processes - defines valid states and transitions between them
		- Technical details - protocols, ports, IP addresses
		- Data flows between multiple interfaces before they get where they are supposed to be (API, different connectors, DB interface)
- Hardware - Infrastruktura, cloud/on premise

![[Pasted image 20240512185649.png]]

## Process Classification Framework
0. Business Functions (enterprise functions)
1. Process Groups (defines groups of processes)
2. Core Business Process (defines roles and high-level functions)
3. Business Activity (defines activities within the process)
4. Business Task (Executed by a single actor - human/actor)
5. Business Step
## Integration
There needs to be a clear definition of an interface:
- Use either standardized solutions
- mediators where it does not work out

# Service
## Business definition
Service accomplishes something in the system that brings value
## Conceptual definition (Characteristics)
- Encapsulation  - the implementation is hidden and not needed for usage
- Reusable - the service can be used by different agents under different scenarios
- Loosely coupled - service does not depend on the requester and other way around; no hard-wired information
- Contracting - Requester and service both agree on an interface between them
- Abstraction - Service interface is abstracted away from the implementation
- Discoverability - Requester can discover the service and understand how to use it
- Composability - Services can be composed together to achieve a more complicated process
## Logical definition
service has a interface, description and implementation
service = interface + implementation
## Architectural definition
Business service - external, exposes functionality of an application
Infrastructure service - internal, supports other services

## Integration
Is a process of connecting applications/services so they can share information and functions.

## Interoperability
Ability of two applications or services to understand each other
- Data - syntax/structure, semantics
- Functions/Processes - syntax semantics
- Technical - protocols, IP addresses

# REST
It is a architectural style which defines contraints to achieve better design:
- Client/server
- statelessness
- cacheability
- layered system
- uniform interface
and following principles:
- identification of resources
- self-descriptive messagess
- HATEOAS

## Resource
anything - real object or abstract thing
they are one or more things in the data model
they are transferred in a message
each resource has an identifier and a representation

## Accessing a Resource
1. Dereference a URI
	- process of creating the request
2. Service processes the request
	 - returns the representation of the current state of the resource
 3. Client receives
	 - client interprets the representation based on the specification
### URI
could be URL or URN
`scheme://authority/path?query#frag`
scheme not protocol - mailto, authority - registered name (eg domain name), path hierarchal form, query non-hierarchal form
fragment - secondary resource identification
#### Path
provides a view on the model, can be chosen different ways to access the same resource. 
#### Query
can define selection, projection, other processing instructions
### URL
For identifying resources and their location to access - network location
### URN
requires to be globally unique and persistant (even if it stops existing)

## Representation
XML, HTML, JSON, YAML, RDF

Content-Type and Accept HTTP Headers can be used to agree on the format
Status code can be used to convey the result type (success, error)

There are different HTTP methods to specify the operation with the resource

## Operations
- Safe - do not change the state of the resource
	- GET
- Unsafe - change the state of the resource
	- POST, PUT, DELETE
- Idempotent - invoking the same method yields the same output
	- GET, PUT, DELETE
- Non-idempotent - invoking multiple times gives different results
	- POST

## HATEOAS
Links to provide context


# HTTP
## 3-Way Handshake
1. Client sends SYN - connection request
2. Server responds SYN ACK
3. Client sends ACK
Result is a socket: (src_ip, src_port, dst_ip, dst_port)

## Latency
- RTT (Round Trip Time) - request + response

## TCP Fast Open
The first request is as normal with a 3-way handshake. Server also sends a cookie for TFO

For further requests the client sends the cookie which the server verifies. If it is valid then it sends the data along with the SYN_ACK response.

## Keepalive
Established connection used for multiple requests/responses
Avoids the 3-way handshake for TCP for multiple requests (the first is still needed)
For each further request it saves one RTT

## HTTP Pipelining
1. Requests are sent without waiting for the response using the same TCP connection
2. Server responds in order in which the requests came in
### Head of line blocking
If a request is taking too long than all the subsequent requests will be delayed. The subsequent responses need to be buffered to wait until they can be sent, which takes resources.

## Multiple TCP connections
Each browser can sent 6 connections per host. We can use sharding to avoid this problem - different subdomains to the same host.

# SOAP vs REST
REST is independent of format
SOAP uses XML

SOAP exposes actions/functions/operations
REST exposes 

SOAP stateful
REST stateless

SOAP message:
- container for the message
- header - metadata to describe the message
- body - payload

WSDL is used to define the interface:
- types: information model
- portType: set of operations
- binding: how are messages transferred (HTTP, SMTP, FTP)
- service: endpoint
They can either be abstract - only types and portType are provided; or concrete - provide everything