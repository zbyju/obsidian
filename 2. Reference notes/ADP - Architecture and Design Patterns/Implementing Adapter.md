1. We have two incompatible interfaces
	- Service that we can't change (3rd party, legacy, lots of dependencies)
	- Client class that wants to communicate with the service
2. Declare the interface of the client
	- The methods that it wants to communicate with service (consume the service by a parameter)
3. Create adapter class that has the service as a field