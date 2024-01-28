# Pros
- [[Open-Closed Principle]] - you can add new strategies without breaking existing code
- You can replace inheritance with composition
- Isolate implementation details to a separate class
- You can change strategy at runtime

# Cons
- If you have just a couple of algorithms and they rarely change, it is an overkill
- Clients need to be aware of the differences between the strategies to know which one to use
- Modern languages solve this problem using anonymous functions that you can pass to the object.

# Use Cases
- Changing strategy at runtime
- Having different strategies that we want to separate and not have in one big class

[[Strategy Pattern]]