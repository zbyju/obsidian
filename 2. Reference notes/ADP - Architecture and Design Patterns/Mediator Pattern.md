Lets you reduce chaotic dependencies between objects. It restricts direct communications between objects and forces them to use a mediator to pass notifications through.
# Example
Imagine a chat application where users can send messages to each other. Instead of users communicating directly, they send their messages to a central server (the Mediator), which then forwards these messages to the intended recipients. In this case, each user is a 'Colleague', and the server acts as the 'Mediator'.
# Diagram
![](https://i.imgur.com/JbmoqtA.png)
1. Components are various classes that contain some business logic. Each contain a reference to a mediator interface. The component isn't aware of the actual class of Mediator - you can give it different mediators to alter the behavior.
2. Mediator interface declares methods of communication with components - usually just has a `notify` method. Components may pass context as parameters (they can pass themselves, but watch out for tight coupling).
3. Concrete mediators often keep references to all components they manage (they might even manage their lifecycle).
4. Components must not be aware of other components. If something happens in/to another component it must only notify the mediator. Mediator then knows where the notification is coming from and triggers some other component.
	- It's a black box to the components
		- They don't know who they are notifying
		- They don't know who notified them

[[Behavioral Patterns]]