Lets you construct complex objects step by step. Allows you to produce different types and representations of an object using the same construction code.

# Example
Meal ordering system (offering `VeganMeal`, `MeatMeal`) each consisting of several components: main dish, side dish, drink, ... The builder allows users to construct their meal step by step.

# What Problem it Solves
- Making complex objects with multiple parts/components
- Allows constructing objects with different representations using the same construction code

# Diagram

![](https://i.imgur.com/em7Ytlc.png)
1. Builder interface declares construction steps
2. Concrete builders provide different implementations of the construction steps. They may produce products that don't follow the common interface.
3. Products are the resulting objects; they don't have to share a common parent, they can be completely different/
4. Optional Director defines the order - basically defines predefined ways of constructing products
5. Client Associate the builder with a director

[[Creational Patterns]]