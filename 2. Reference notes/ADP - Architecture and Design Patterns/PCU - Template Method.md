# Pros
- Simplify an algorithm and allow its changes
- Reduce duplicate code by extracting into a superclass
# Cons
- Might violate Liskov Substitution Principle - the subclass might override the steps in a way the breaks the client code
- The provided skeleton might be limiting
- They tend to be hard to maintain the more steps they have
# Use Cases
- Overall structure of an algorithm is clear, we just need the steps to be customizable


[[Template Method Pattern]]