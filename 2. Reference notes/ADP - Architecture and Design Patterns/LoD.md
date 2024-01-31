The Law of Demeter (often termed "principle of least knowledge") is a design principle, which encourages objects to only communicate with their immediate neighbours. It promotes the idea that an object should only have limited knowledge about other distant objects.

# Example
Consider an object `A` that uses an object `B`, which in turn uses an object `C`. The Law of Demeter suggests that `A` should not directly invoke methods on `C`. So, rather than doing something like `a.getB().getC().doSomething()`, `A` should request `B` to perform the operation which might involve `C`.

# Description
By adhering to the Law of Demeter, software tends to be more modular and maintainable. Objects remain loosely coupled, which makes the system more adaptable and reduces unforeseen side effects.

[[Design Principles]]