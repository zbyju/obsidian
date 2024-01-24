(also known as Virtual Constructor)

Provides interface for creating objects in a superclass but allows subclasses to alter the type of objects created.

# Example
We have a `Logistics` class that creates transport objects. The type of the transport object is determined by subclasses - either `Truck` or `Ship`.

# What Problem it Solves
- Decouples creation of objects from their use

# Diagram
![](https://i.imgur.com/W3bv38T.png)
1. Declare product interface that is common for all products
2. Concrete products are different implementations
3. Creator class has a method that returns new product objects (it has to return the abstract product)
	 - This class usually has some business logic related to products
	 - but it also creates products
		- Despite its name it's not the main purpose
4. Overrides the methods for creating products
	- They can use the default implementation of the Creator for other operations (business logic) 

[[Creational Patterns]]