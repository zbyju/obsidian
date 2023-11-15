- A behavioral design pattern that allows capturing and externalizing an object's internal state so that the object can be returned to this state later.
- Facilitates undo or rollback capabilities by storing previous states of an object without exposing its internal structure.
- Goes well with Command pattern

Improves Principles:
- Encapsulation
- Single Responsibility

*Example: Text editor: the Memento pattern can be used to implement undo functionality. Each change in the text is saved as a memento object. When the user wants to undo an action, the editor restores its state from these mementos, enabling backward navigation through the changes.*

**Linkage:**
- [[_ADP Reference]]