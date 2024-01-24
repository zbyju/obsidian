Ensure class has only one instance while providing a global access point to it.

# Example

# What Problem it Solves
1. Allowing only one instance of a class
2. Providing global access to it

# Diagram
![](https://i.imgur.com/gs8UL6A.png)
1. The singleton class declares a static method `getInstance` that on first call creates the instance and then for all the following calls just returns the already created instance
	- It should have a private or hidden constructor - allow access only to the static method

[[Creational Patterns]]