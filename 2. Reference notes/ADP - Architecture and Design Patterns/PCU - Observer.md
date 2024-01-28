# Pros
- Promotes loose coupling
- [[Open-Closed Principle]] - You can add new subscriber objects and observers without breaking previous code
- You can establish relations at run time
# Cons
- Subscribers are generally notified in a random order
- There can be memory leaks if poorly implemented
# Use Cases
- Great for UI handling
- Good when we need to establish relations at run time

[[Observer Pattern]]