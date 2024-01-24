1. Private static field that will hold the instance
2. Public method for getting the instance
3. Implement using lazy initialization - first call initializes, others retrieve.
	- Use [[Double Check Locking]] in multithreaded environments
4. Make the constructor private to disallow other instances to be created
5. Refactor other code to use the `getInstance` method

[[Singleton Pattern]]