# Pros
- You can be sure that a class has only one instance
- Gain global access to it
- Save resources as you only have one resource

# Cons
- Violates the [[Single Responsibility Principle]] - it packs the business logic with the singleton functionality
- Requires special treatment in a multithreaded environment
- It may be harder to test things - constructor is private which might not work with some frameworks

# Us