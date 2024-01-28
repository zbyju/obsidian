# Pros
- [[Single Responsibility Principle]] - organize code related to particular states into separate classes
- [[Open-Closed Principle]] - adding new states doesn't break existing code
- Simplifies complex state machine classes
# Cons
- Applying this might be overkill for simple state machines
# Use Cases
- When the object we are working with has clear-cut states that it transitions between
- When the state specific behavior is complex and we want to simplify it

[[State Pattern]]