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
1. Use Cases
2. Controllers
3. External Interfaces

[[Architectures]]