(also know as: Snapshot)

Lets you save and restore previous state of an object without revealing the details of its implementation.

# Example
Text editor that allows for undoing changes to text:
1. Originator = TextEditor = Class that represents the text editor and has the state
2. Memento = TextSnapshot = Hold the text state when saved
3. CareTaker = UndoFeature = Reponsible for keeping all the mementos

# Diagram
![](https://i.imgur.com/nVIjo3T.png)
1. Originator can produce snapshots of its own state as well as restore its state from snapshots when needed.
2. Memento is a value object that acts as a snapshot.
3. Caretaker knows when and why to capture the originator's state, but also when the state should be restored.
4. Caretaker can keep track of the originator's history by storing a stack of mementos.