Thread of execution = exectutes code line by line
Saves data (variables) to memory
- identifier (name of the variable)
- value
	- primitive value
	- for a function it means storing the body of the function
	- if i wanna store function call then we
		- first store it as uninitialized
		- then compute the function and store the value
- more information
	- const/let

Execution context = it is created to run a code of a function:
- thread of execution
- memory
There is a "global" execution context and then with each function call there is a new "local" execution context created.

Functions take in values - the identifier is called parameter, the value of the parameter is called argument.


There is always just one thread of execution "active" => we can't do more than 1 thing at a time


Call stack = keeps track of what function is currently running
Each function call adds a new entry to the call stack
Each return from a function pops the latest entry from the call stack
The topmost entry in the call stack is the function that is currently executing
The bottommost entry is the "global"/"main" function

When defining functions we want to make them as general as possible to make them reusable.
- Pass data through arguments to the function
	- values
	- functions
		- = higher order function

In javascript functions are first class citizens/objects - they are treated as any other type of value

Higher order function = takes in a function (or returns a function)
Callback function = the function that is passed as an argument to a function (to a higher order function)

Arrow function = shorthand for saving a function to a variable

Closure

With each function definition we get a new execution context with its own variable environment (V.E.).

When defining a new function it has access to all the variables within its scope
- Since javascript is a statically scoped (lexically scoped) language
	- = scope is determined by where the function was declared
	- dynamically scoped would mean the scope of the function would be determined by where the function is called
- When we store this function somewhere it needs to bring this data as well so that it can interact with the variables when it is called (even after the original execution context is deleted)

![[Pasted image 20240813234736.png]] 

This can be great for:
- Singleton/once
	- Run function only once
	- Run function once and then on next runs do something else
- Memoization
	- Remember value of a call, next time only return memoized value
- Module pattern
	- instead of polluting global namespace we can have modules with data for the lifespan of our app
- async javascript
	- when we eventually comeback it returns running