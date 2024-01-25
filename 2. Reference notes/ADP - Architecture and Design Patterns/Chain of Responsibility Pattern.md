Lets you pass request among a chain of handlers. Each handler decides to either process the request or to pass it to the next one.
# Example
A request from a customer goes through a chain of handlers that check if the request is valid. Each handler can say that it is not, or if the request passes the test it gets sent to the next handler.
# Diagram
![](https://i.imgur.com/zC2GDSK.png)
1. There is a Handler interface that all handlers follow. It should have a method `handle` but can also have other methods such as `setNext`.
2. Optionally there is a Base Handler, there can be some boilerplate implementation that is common for handlers.
3. Concrete handlers implement the actual handle method
4. Client can compose the handlers however they want; or even dynamically. The request can be passed to any handlers (doesn't have to start with the first one)

[[Behavioral Patterns]]