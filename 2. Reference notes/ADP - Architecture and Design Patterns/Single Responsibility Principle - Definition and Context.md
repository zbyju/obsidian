**Definition**: A class should have only one reason to change, meaning it should have only one responsibility.

**Example**: A "User" class in a software system should only handle attributes and behaviors related to a user, like "Name" or "Login()". It shouldn't be responsible for, say, logging user activities; that would be another class's responsibility, like "UserActivityLogger".

**Description**: SRP ensures that a class adheres to one functionality, leading to a more organized system where changes in one area don't unexpectedly affect others.

**Linkage:**
- [[_ADP Reference]]
- [[SOLID - Definition and Context]]