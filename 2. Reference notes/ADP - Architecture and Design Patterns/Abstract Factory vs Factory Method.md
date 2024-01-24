# Factory Method
- Adds creating objects directly to a class with business logic
	- This enhances the possibilities the class can be used
		- Depending on which implementation of the class we use it will operate over different products

# Abstract Factory
- Its only purpose is creating products
- Each factory implementation focuses on creating all product types of a single variant
- Business logic is somewhere else


Factory Method can be used at the start, but then can be split into a method with business logic using an abstract factory to separate concerns and clean the code.

[[Abstract Factory Pattern]]
[[Factory Method Pattern]]