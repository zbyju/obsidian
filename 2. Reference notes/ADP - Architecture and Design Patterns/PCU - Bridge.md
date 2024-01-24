1. What operations the client needs to work with and add them to the interface
2. Identify what operations the abstraction needs from the implementation
3. Create all the implementation classes for all platforms following the interface
4. Inside the abstraction create a reference to the implementation
5. Optionally create refined abstraction if there are more variants
6. The client passes the implementation to the abstraction through the constructor, then works only with the abstraction.

[[Bridge Pattern]]