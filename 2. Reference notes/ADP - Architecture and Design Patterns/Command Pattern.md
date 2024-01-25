(also known as Action, Transaction)

Turns a request into a standalone object that contains all information about the request. This way you can pass requests as method arguments, delay or queue request's execution, support undoable operations.
# Example
Let's consider a remote for a TV. Each button can focus on its functionality, but it produces some Command that can then get interpreted somewhere else. This way buttons can even change functionality; or the same functionality can be assigned the different buttons by just setting the appropriate command.
# Diagram
![](https://i.imgur.com/IUyn1Kx.png)
1. Invoker (sender) is responsible for initiating the requests. It has a method to receive the command and then a method to execute the command.
2. Command usually has only one method for executing it
3. Concrete commands implement various requests. The command isn't supposed to execute the code itself; it should pass it to someone class with business logic (or these 2 classes can be merged). Parameters for executing the command can be fields.
4. Receiver class contains some business logic. The command handles how the request is passed to the receiver; receiver does the work.
5. Client configures different command objects - it needs to pass all the necessary parameters into a constructor. Then it can be associated with different invokers.

[[Behavioral Patterns]]