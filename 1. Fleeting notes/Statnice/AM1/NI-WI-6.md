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

## DNS 