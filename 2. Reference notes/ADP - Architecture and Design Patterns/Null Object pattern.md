- A behavioral design pattern that uses an object with defined neutral ("null") behavior as a substitute for the absence of an object.
- Prevents null reference errors by ensuring an object always has a valid reference to an instance, albeit one that performs no action.

*Example: GUI: a null object could represent a default, do-nothing behavior for an event listener. Instead of checking if a listener is null before calling an event method, the GUI always calls the method, and the null object ensures that nothing happens if there's no real behavior to execute.*

[[Non-GoF Patterns]]