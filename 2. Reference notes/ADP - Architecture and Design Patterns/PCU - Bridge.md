# Pros
- Simplifies working with low level implementations (or even harder to work with interfaces)
- [[Open-Closed Principle]] - you can add/remove abstractions and implementations independently
- [[Single Responsibility Principle]] - You can focus on implementing a low level solution and then separately making a nice interface to work with it
# Cons
- The code might become more complicated
# Use Cases
- Implementing platform independent classes and apps
- When changes in implementation shouldn't effect the abstraction and vice versa.

[[Bridge Pattern]]