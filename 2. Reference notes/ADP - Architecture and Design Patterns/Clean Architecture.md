Focuses on separation of concerns, making system easier to manage and test. Its primary goal is to create systems that are independent of frameworks, UI, database and other external agency.

# Independent of frameworks
Frameworks should be tools and shouldn't dictate the architecture.

# Testable
Business rules should be testable without UI, database, web server or any other external element.

# Independent of UI
UI can be changed easily without changing the rest of the system.

# Independent of Database
Business rules are not effected by changing the database.

# Independent of external agency
Business rules simply don't know anything about the outside world. They live on their own.


![](https://i.imgur.com/y1faDjc.png)
0. Dependency rule
	- Source code dependencies can only point inwards. Nothing from an inner circle can know anything about anything from an outer circle (includes functions, classes, variables, ...)
	- We don't do anything in outer circles to impact inner circle
1. Entities
	- Basic building blocks used for enterprise wide business rules
	- Or just business objects of the application
2. Use Cases
	- These include application specific business rules. It encapsulates and implements use cases - these define data flow between objects
3. Interface adapters
	- These adapters convert data from formats most convenient for use-cases and external agencies
4. Frameworks and drivers
	- This is where the details go - web, database, etc.
	- This is more of an infrastructure layer

There is no rule that says these need to be the layers (there doesn't have to be 4 layers), you always need to follow the dependency rule.

Typically, the data that crosses boundaries should be very simple data structures.

[[Architectures]]