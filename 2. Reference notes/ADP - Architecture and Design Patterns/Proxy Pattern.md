- A proxy not only serves as a stand-in for another object but can also extend or augment its functionality.
- Common enhancements include logging, caching, authentication, lazy loading, and optimizing database connections.
# Example
Database access class: implementing a standard data access interface, can be wrapped by a proxy that adds caching, thus improving performance by avoiding frequent database hits. 
Another proxy might add logging to monitor database queries, aiding in debugging and performance tuning.

# What Problem it Solves

# Diagram
![](https://i.imgur.com/xELYOcA.png)


[[Structural Patterns]]