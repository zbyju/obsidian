**Infrastruktura middlewaru. Metriky pro měření výkonu služby. Prvky pro rozložení zátěže (load balancers).**

# Types of Middleware
## Scalability
Improving performance of the application and scalability
- Message brokers
- Load balancers
- Proxy servers, Reverse proxy
## Functional
They help achieving better integration and inner workings of the application
- Process servers
- Mediators
- Repositories, Registries
- Monitoring solutions
## Security
- Firewalls
- Gateways
# Metriky pro mereni vykonu
## Response time
- client-side metric
## Queries/Requests per Second
- server-side metric
- caching may improve it

# Load balancers
Distributing load to multiple nodes
Can try to equal the load or prefer some nodes
Healthchecking to not send data to a dead node

## DNS LB
A-record can have multiple IP addresses, round robin algorithm will then split the load
- Very simple
- IP addresses get cached and can take hours to redistribute the load
- Can’t do any further optimizations based on load or health
## Reverse-Proxy LB
Reverse-proxy chooses the app instance, it can do so based on load, healthchecks.
- More comprehensive - based on current load, health
- Problems with having the same user using the same server - for stateful operations

### Session state
#### Sticky cookie
Users get cookies that they identify with for reverse-proxy to choose which server to choose for that user to persist the session.

#### Session in DB
Another approach is to store the session information in DB

#### In-memory replication
Primary server holds the data in-memory, the other is replicating it

### Healthchecking
Send multiple requests to the service, based on the success rate either keep using the server or stop using it

### Strategies
- Roundrobin: send to the first, then second, then third; then last and then first again, …
- Choosing randomly based on weights
- Choosing based on least connections
- Choosing based on the lowest average response time.
- Limiting the maximum number of connections to a server
- Slow-start - recently recovered servers will not get overwhelmed
## Client-side LB
Client determines which server it is going to use