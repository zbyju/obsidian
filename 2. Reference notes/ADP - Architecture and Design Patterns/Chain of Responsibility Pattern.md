Lets you pass request among a chain of handlers. Each handler decides to either process the request or to pass it to the next one.

# Example

# What Problem it Solves

# Diagram
![](https://i.imgur.com/zC2GDSK.png)
1. There is a Handler interface that all handlers follow. It should have a method `handle` but can also have other methods such as `setNext`.
2. Optionally there is a Base Handler, there can be some boilerplate implementation that is common for handlers.
3. Concrete handlers implement the actual handle method
4. Client can compose the 