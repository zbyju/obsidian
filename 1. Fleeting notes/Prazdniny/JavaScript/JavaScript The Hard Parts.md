# Javascript Principles
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

# Closure

With each function definition we get a new execution context with its own variable environment (V.E.).

When defining a new function it has access to all the variables within its scope
- Since javascript is a statically scoped (lexically scoped) language
	- = scope is determined by where the function was declared
	- dynamically scoped would mean the scope of the function would be determined by where the function is called
- When we store this function somewhere it needs to bring this data as well so that it can interact with the variables when it is called (even after the original execution context is deleted)
	- It brings its own backpack that stores all the needed variables (references to them) for its execution
	- This backpack is called the closure
	- It is stored in the `[[scope]]` property

![[Pasted image 20240813234736.png]] 

This can be great for:
- Singleton/once
	- Run function only once
	- Run function once and then on next runs do something else
- Iterator
	- Get a data structure and return a function that will give us the next value each time.
	- Remember where we are inside the iteration.
- Generators
- Memoization
	- Remember value of a call, next time only return memoized value
- Module pattern
	- instead of polluting global namespace we can have modules with data for the lifespan of our app
- async javascript
	- when we eventually comeback it returns running
### Generators

They are special functions that let us "pause" execution of a function and remember where we left off. They need to be denoted as `function*`

![[Pasted image 20240815003038.png]]
The first call `createFlow()` returns an object `{ next: fn }`
This object is then used to call `next`
`yield` keyword immediately returns the value
next time we get to pass the 2 where the yield left off (newNum is initialized to 2)

This is done using a similar concept to closures. Javascript uses the `[[generatorLocation]]` which stores the line number where we left off.

These functions are also special because their execution context is not deleted; they continue where they left off with the data they had.

#### Async generator
![[Pasted image 20240815004226.png]]
This is basically how `await` works. The yield returns a promise object. We add a callback to the promise object. When the promise resolves the callback is called and the functio `doWhenDataReceived` passes the data back to the function and the function continues in executing.

When using the `await` keyword javascript automizes this process for us.

# Async
Code in javascript is executed line by line (with jumps to functions).

Code that would take too long waiting for external resources (File I/O, network requests) can block the main thread
- = we would just be waiting for that request to finish and then continue = no execution is done

Therefore we have async operations

These functions usually take parameters needed for their execution + callback. This callback is a function that is executed when the function finishes (not immediately after!).

When the async function is resolved (done) the callback is added to the callback queue.

The callback is called when:
1. Async function is done (request is done, IO is done, timer is done)
2. And there is nothing on the call stack (no function is being run).
3. It is the first in the queue of callbacks

The callback is called and starts executing its code synchronously again; then when it's done we get another callback from the callback queue.

Therefore the callback can be called pretty late if there is some heavy computation being done

```js
console.log(1)

function asyncFun() { setTimeout(() => console.log("async"), 0)}

function heavyComputeFun() { /* Do some heavy computation (without IO) for 1s */ }

asyncFun()

heavyComputeFun()

console.log(2)
console.log(3)
console.log(4)

// 1
// ... heavyCompute is executing for 1s ...
// 2
// 3
// 4
// async
```
Because the main thread has still stuff to do, it never executes the asyncFun callback in the setTimeout; it does that as the last thing when everything else finishes.

This is called the event loop.

```js
console.log(1)


function asyncFun2(i) { setTimeout(() => console.log("async2 " + i), i)}

function asyncFun(i) {
    setTimeout(() => {
	    heavyComputeFun()
	    console.log("async " + i)
	}, i)
}

function heavyComputeFun() { 
    let sum = 0
    for(let i = 0; i < 1000000000; i++) { sum += i }
    return sum
}

asyncFun(0)
asyncFun(10)
asyncFun(0)
asyncFun(0)
asyncFun(10)

heavyComputeFun()

asyncFun2(0)
asyncFun2(10)
asyncFun2(0)
asyncFun2(10)

console.log(2)
console.log(3)
console.log(4)

// First code in global() is executed (1,2,3,4) + all timers are ran
// Callbacks from timers are added to the callback queue in the order or execution + delay
// Callbacks are starting to get executed from first to last (first delay 0, then delay 10)

/*
1
2
3
4
async 0
async 0
async 0
async2 0
async2 0
async 10
async 10
async2 10
async2 10
*/
```

# Promises
Promise is an object in javascript that is used for async functions. It is an object that can be used to interact with future values.

It offers the method `then` that takes a callback that is executed when the promise is resolved (successfully).

It also offers `catch` method that takes a callback that is called when the promise is rejected (failure).

In fact there are two types of callback queues - Microtask and Macrotask queues:
- Microtask queue - callbacks from promises, async functions, fetch, ...
- Macrotask queue - callbacks from timers - setTimeout, setInterval, setImmediate

We first go through all the microtasks and then all the macrotasks.

![](https://media.licdn.com/dms/image/D5612AQHIuZDc3cqPtg/article-cover_image-shrink_720_1280/0/1721185522661?e=1729123200&v=beta&t=e-9VEg9CC2Te5DbzaVx8foVQx2PlhqjoNVGDVE-rtS0)

![[Pasted image 20240814215833.png]]![[Pasted image 20240814220156.png]]

# OOP

## Objects

We can create an object and define the properties with their values.
If the value of a property is a function then we call it a method.

```js
const user1 = {
	name: "Will",
	score: 3,
	increment: function() { user1.score++ }
}

// This effectively does:
const user1 = {} //or Object.create(null)
user1.name = "Will"
user1.score = 3
user1.increment = function() { user1.score++ }
```

We can also use `Object.create(obj)`. This function creates an empty object, but sets the passed object as its prototype.

To improve DRY we can create a factory function. This function takes parameters and creates the object for us

## Prototype chain
Instead of each object having to implement all its functions we can create an object that the other objects use as their prototype. If the requested functionality (say .decrement()) is not found in the object, javascript will look through the prototype chain to find if the functionality exists.

The link is created using `Object.create(object)`

The prototype object is stored in a property called `__proto__` which contains the reference to the prototype object. Each object has a `__proto__` property (Object.prototype is a parent of everything)

### this
On each method of an object there is an implicit variable already predefined called `this` which is a reference to the object that the method was invoked on.

#### Problems
```js
const obj = {
	increment: function {
		function add1() { this.score++ }
		add1()
	}
}
```

Even tho javascript should look in the execution context of:
1. add1
2. increment
3. global
and find `this` defined in the increment function pointing to `obj` it doesnt do that.

A new function declaration overrides `this` and sets it to the global `this` which is `undefined`.
##### Solutions
1. this = that
```js
const obj = {
	increment: function {
		const that = this
		function add1() { that.score++ }
		add1()
	}
}
```
2. .call(thisArg)
```js
const obj = {
	increment: function {
		function add1() { this.score++ }
		add1.call(this)
	}
}
```
3. Arrow function
Arrow functions scope `this` lexically and therefore it fixes this issue.
```js
const obj = {
	increment: function {
		const add1 = () => { this.score++ }
		add1()
	}
}
```
### Object.prototype
`Object.prototype` is an object that is a parent of all objects and it contains some useful properties other objects can utilize. Its value of `__proto__` is `null`.
- hasOwnProperty 
### new
Instead of using a factory function we can use the keyword new which does:
1. Creates the object
2. Returns the object
3. Creates the prototype link to an object


Functions are also objects
![[Pasted image 20240814234059.png]]Each function has a `prototype` property that is initialized to an empty object.
We can use this property to put our prototype object there (or define properties on this object).
When we then call the function with the `new` keyword it puts this object inside the `prototype` property on the function inside the prototype chain on the newly created object.

```js
// Comments = old way of doing it without `new` keyword
function userCreator(name, score) {
	// const newUser = Object.create(userFunctionStore)
	/* newUser.score */ this.name = name
	/* newUser.name  */ this.score = score
	// return newUser
}

/*
function userFunctionStore = {
	increment: function() {this.score++}
}
*/
userCreator.prototype.increment = function() {this.score++}

// const user1 = userCreator("Eva", 9)
const user1 = new userCreator("Eva", 9)
```

the `new` keyword enhances our function by:
1. Creating an empty object and assigning it to `this`
2. Assigning the `__proto__` property on this to the `property` on the function
3. Executes the function (usually the function assigns properties on `this`)
4. returns `this


There is a problem that when we see this function it is not clear right off that we need to use the `new` keyword when calling it. Solutions:
1. Capitalize the name
	- Use `UserCreator` instead
	- Not enforced but a good habit
2. Use `class` keyword instead
	- Just syntactic sugar for all of this

### Class
They combine the property and method declarations to a single place. 

![[Pasted image 20240815000209.png]]

There is a special `constructor` method that we can use to initialize our data.