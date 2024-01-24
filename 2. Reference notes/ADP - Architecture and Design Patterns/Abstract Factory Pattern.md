It produces **families** of related objects without specifying their concrete class.

We have product types and variants of these products. There is a factory for each product variant producing all product types we have.

# Example
Abstract factory making furniture. There are two implementations of this factory: `SphericalFactory` and `PyramidalFactory` each making furniture but producing them in different shapes.

Product types: Chair, table
Variants: Spherical, Pyramidal

# What Problem it Solves
- It helps managing and organizing families of related objects
- Ensures products are compatible across variants
- Abstracts and separates away object creation

# Diagram
![](https://i.imgur.com/yGY9m1P.png)
1. Abstract Product declaring the interface of the products
2. Implementation of the products
3. Abstract factory declaring the interface of what it is able to produce
4. Implementations of factories producing products of different types
5. Consumer has an abstract factory calling functions that produce abstract products

[[Creational Patterns]]