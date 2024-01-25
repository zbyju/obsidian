Defines skeleton of an algorithm in a class and then lets subclasses override specific steps without changing its structure.

# Example


# Diagram
![](https://i.imgur.com/P7KZeZS.png)
1. Abstract Class declares methods that act as steps of an algorithm as well as the actual template method which calls these method in a specific order. These steps might be either abstract or have some default implementation.
2. Concrete classes override the steps; but not the template method.