(also known as: Listener, Event-Subscriber)

Lets you define a subscription mechanism to notify multiple objects about any events that happen to the object you are observing.

# Example

# Diagram
![](https://i.imgur.com/pPj02lx.png)
1. Publisher issues events of interest to other objects. These events occur when the publisher changes its state or executes some behaviors. Publishers have some way for subscribers to join and leave the list.
2. When a new event happens the publisher calls the notification method declared in the interface.
3. Subscriber interface declares a notification interface. In most cases it's just a update method; this method might have some context as parameters that the publisher sends over as well.
4. Concrete Subscribers perform actions based on the notifications they receive.
5. Subscribers get context through arguments of the method
6. Client creates a publisher and subscriber objects separately and then registers subscribers to the publisher.

[[Behavioral Patterns]]