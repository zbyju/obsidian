# Pros
- [[Single Responsibility Principle]] - cleans up code by extracting traversing algorithms into separate classes
- [[Open-Closed Principle]] - you can implement new collections and iterators without breaking existing code
- Iterators contain their own state - you can have multiple iterators over the same collection
	- You can even iterate over the collection in parallel
	- You can delay iteration and continue later
# Cons
- Applying it might be overkill
- It may be less efficient
- It might hide complexity
# Use Cases
- Common collections (usually already implemented)
- Providing a way to iterate over some structure without the client knowing how; or even how it looks like


[[Iterator pattern]]