(also known as Clone)

It lets you copy existing objects without making your code dependent on their classes.

# Example
Graphic design software where users might want to duplicate circles, squares, etc. Each shape is a prototype that allows duplicating it.

# What Problem it Solves
- 

# Diagram
![](https://i.imgur.com/3ay9vJc.png)
1. Prototype interface declare cloning methods - usually just `clone()` method.
2. Concrete prototype implement the cloning method
3. Client can produce a clone of any object

[[Creational Patterns]]