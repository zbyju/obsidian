**Asynchronní I/O a JavaScript (stack, heap, queue, event loop). Node.js. Srovnání se synchronním I/O. Protokol HTTP/2.**

# Asynchronous IO
A style of concurrent programming
Single threaded, uses cooperative multitasking

Tasks are ran through event loop
Task is able to “pause” when it is waiting for a result, data and let other tasks to be run in the meanwhile
This way it feels like concurrent execution

## Synchronous
Relies on threads to achieve concurrency, otherwise:
each IO blocks the whole execution until data is retrieved

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
- every IO is non-blocking (async)
One worker thread to process requests, no need to deal with concurrency problems
open-source

The event loop goes through phases:
1. Timers
	- Executes setTimeout and setInterval callbacks
2. I/O callbacks
	- executes IO callbacks except close callbacks
3. idle/prepare
	- used internally
4. poll
	- retrieve new IO events
5. check
	- invoke setImmediate() callbacks
6. close callbacks
	- executes close callback socket.on(“close”, …)

# HTTP2

## TLS Handshake
0. TCP 3-way handshake happens
1. Client sends ClientHello (SSL/TLS versions, cipher suites)
2. Server sends:
	1. ServerHello (Highest SSL/TLS version, cipher suite)
	2. Certificate
	3. ServerHelloDone
3. Client validates the certificate and sends encrypted secret
4. Server computes session key
## Establishing Connection
- Client asks to use the HTTP2 protocol in the ClientHello message
- Or client upgrades from a plaintext connection using 101 Switching protocols
- Or client has prior knowledge (eg. internal service) and starts with HTTP2 and fallsback to HTTP1.1
## Binary Framing
Everything is sent using binary format
Messages are sent in frames - Headers frame (Request Line, headers), data frame (body)
Frames are identified by the message they belong to (to a stream)
Communication is multiplexed within a single TCP connection
#### Stream
Bi-directional flow of bytes in connection
May carry one or more messages
May have priority
#### Message
Sequence of frames
It’s the request or response
#### Frame
Smallest unit
Each has a header to indetify its stream
- length
- type (DATA, HEADER, PRIORITY, SETTINGS, …)
- flags - frame-type specific boolean flags
- stream identifier
## Multiplexing
HTTP/1.1 used pipelining which had head of the line blocking; browser could only have 6 connections
HTTP/2 allows for multiplexing: requests and responses can be sent in any order. The order is important within a stream which they are identified by
Advantages:
- interleave multiple requests and responses - no blocking
- single tcp connection - multiple requests and responses can be delivered in parallel
- lower page load times
- improve utilization of network capacity

## Flow Control
The client and the server can set a window size of how much data it can send at once before waiting fo

