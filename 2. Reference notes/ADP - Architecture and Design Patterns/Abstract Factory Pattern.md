It lets us produce **families** of related objects without specifying their concrete class.

# Example
Abstract factory making furniture. There are two implementations of this factory: `SphericFactory` and `PyramidalFactory` each making furniture but producing them in different shapes.

# Diagram
![](https://i.imgur.com/yGY9m1P.png)
1. Abstract Product declaring the interface of the products
2. Implementation of the products
3. Abstract factory declaring the interface of what it is able to produce
4. Implementations of factories producing products of different types
5. Consumer has an abstract factory calling functions that produce abstract products