1. Create the prototype interface. It has one method - `clone`. Or add it as part of some hierarchy
2. Prototype class must define an alternative constructor that accepts an object of that class as an argument. Such constructor then copies all the values of passed object.
	- If this is not possible then you need to use the clone method
3. The cloning method usually just calls the constructor: `new ConcreteConstructor(this)`
4. Optionally create a prototype registry that holds catalog of frequently used prototypes

[[Prototype Pattern]]