**Definition**: Subtypes must be substitutable for their base types without altering the correctness of the program.

**Example**: If there's a "Bird" class with a function called "Fly", and you have a subclass "Penguin", a Penguin object should still be usable wherever a Bird object is, even though penguins can't fly. This might indicate a flawed design.

**Description**: LSP ensures that a derived class can replace its base class without affecting program correctness, promoting consistent behavior and ensuring reliability.

**Linkage:**
- [[_ADP Reference]]