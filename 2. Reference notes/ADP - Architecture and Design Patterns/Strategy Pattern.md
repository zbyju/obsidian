Lets you define a family of algorithms, put each of them in a separate class, make their objects interchangeable.
# Example
Consider a payment processing system in an e-commerce application:
1. **Context (PaymentContext):** Maintains a reference to a Strategy object and is configured with a ConcreteStrategy object.
2. **Strategy (PaymentStrategy):** Interface that defines the operation(s) that all supported algorithms (concrete strategies) will implement.
3. **Concrete Strategies (CreditCardPayment, PayPalPayment, etc.):** Implement the PaymentStrategy interface with specific algorithms for processing payments.

# Diagram
![](https://i.imgur.com/AX3lnIG.png)
1. Context maintain a reference to one of the concrete strategies via the strategy interface.
2. Strategy interface declares method for context to execute a strategy
3. Concrete strategy implements different variations of an algorithm the context can use
4. Context calls the execution method on the linked object each time it needs to run the algorithm. The context doesn't know which strategy it is using.
5. Client creates specific strategy object and passes it to the context. Context exposes a setter which lets clients to set the strategy or change it during runtime.

[[Behavioral Patterns]]