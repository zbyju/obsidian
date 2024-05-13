**Asynchronní I/O a JavaScript (stack, heap, queue, event loop). Node.js. Srovnání se synchronním I/O. Protokol HTTP/2.**

# Asynchronous IO
A style of concurrent programming
Single threaded, uses cooperative multitasking

Tasks are ran through event loop
Task is able to “pause” when it is waiting for a result, data and let other tasks to be run in the meanwhile
This way it feels like concurrent execution

## Javascript Runtime
- Stack - Function parameters, local variables
- Heap - allocated blocks of memory
- Queue (Event Loop) - list of messages to be processed
	- Message = data + callback
	- Messages completed one by one
	- Each message is completed fully before other messages (if it takes a lot of time, then other things get blocked)

Each runtime has its own stack, heap and queue. iframe and web workers have their own runtimes.
Communication between runtimes can be done using postMessage, while other runtimes listen for the messages

### Web workers
Code runs in a separate thread, can do anything but not manipulate the DOM
Can spawn new workers
They are thread safe
Dedicated workers can only be accessed by the script that created them
Shared workers can be accessed by multiple scripts (iframes, windows, workers)

## Node.js
Javascript Runtime for the backend uses the V8 engine
Uses event driven IO framework
- every IO is non