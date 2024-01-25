# Pros
- [[Single Responsibility Principle]] - Decouple classes that invoke operations from classes that perform them
- [[Open-Closed Principle]] - You can introduce new commands into the app without breaking existing code
- You can assemble simple commands to create a complex one
# Cons
- Code might be more complex
# Use Cases
- Representing various requests as objects to separate concerns.
- When you need to queue, schedule or adjust execution of requests
- When you need to implement undo/redo


[[Command Pattern]]