# Pros
- Clone objects without coupling to their concrete classes
- Get rid of repeated initialization in favor of cloning
- Produce complex objects easier (by cloning or using the [[Prototype Registry]])

# Cons
- Cloning complex objects can have circular references and can be tricky

# Use Cases
- Cloning objects including their private fields
- 