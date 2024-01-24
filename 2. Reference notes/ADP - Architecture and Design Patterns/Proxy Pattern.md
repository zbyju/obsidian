- A proxy not only serves as a stand-in for another object but can also extend or augment its functionality.
- It allows you to do something before or after each request.
- Common enhancements include logging, caching, authentication, lazy loading, and optimizing database connections.
# Example
Database access class: implementing a standard data access interface, can be wrapped by a proxy that adds caching, thus improving performance by avoiding frequent database hits. 
Another proxy might add logging to monitor database queries, aiding in debugging and performance tuning.

# Diagram
![](https://i.imgur.com/xELYOcA.png)
1. Service Interface declares the interface of the service that we want to enhance. The proxy must follow this interface so that we can substitute it instead of the original service.
2. Service class is the original class containing business logic
3. Proxy class has a reference to the real service and it implements methods of 

[[Structural Patterns]]