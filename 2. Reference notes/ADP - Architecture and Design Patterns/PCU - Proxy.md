# Pros
- [[Open-Closed Principle]] - new proxies can enhance the usage without changing the service or clients.
- [[SoC]] - it separates the business logic from some other functionality (caching, access control, ...)

# Cons
- Code can be more complicated
- The response from the service might be slower

# Use Cases
- Caching
- Logging
- Lazy initialization
- Security
- Access Control

[[Proxy Pattern]]