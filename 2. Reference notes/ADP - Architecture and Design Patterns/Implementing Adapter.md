1. We have two incompatible interfaces
	- Service that we can't change (3rd party, legacy, lots of dependencies)
	- Client class that wants to communicate with the service
2. Declare the interface of the client
	- The methods that it wants to communicate with service (consume the service by a parameter)
3. Create adapter class that has the service as a field
	- Usually it takes the service as a constructor
4. Implement the interface methods. It should delegate most of the work to the service and only translate some data/formats
5. Client will use the adapter using the interface. This lets you change the interface, but also add new adapters in the future.

[[Adapter Pattern]]