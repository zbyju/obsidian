Lets an object alter its behavior when its state changes. It appears as if the object changed its class.

They are based on the idea of a Finite Automaton - some context has a state, then we get a request to do some action -> this leads to the context telling the state it should do the action, which it executes and also optionally changes the state of the context.

# Example
We have a music player - it has methods: `lock, play, next, previous`. We have states: `ReadyState, PlayingState, LockedState`. Then we define transitions:
1. `LockedState`:
	1. `lock` then switch context to `ReadyState`
	2. any other method called: do nothing
2. `ReadyState`:
	1. `lock` then switch context to `LockedState`
	2. `play` then make context play music and switch to `PlayingState`
	3. `next`, `previous` then make context go to next/previous and stay in `ReadyState`
3. `PlayState`:
	1. `lock` then switch context to `LockedState`
	2. `play` then stop music and switch to `ReadyState`
	3. `next`, `previous` then go to next/previous, play it and stay in `PlayingState`
# Diagram
![](https://i.imgur.com/b34BYZn.png)
1. Context stores a reference to one of the concrete states and delegates to it the state work. The context communicates with the state object via the state interface. The context has a method for changing state.
2. State interface declares state specific methods - they should make sense for all concrete states.
3. Concrete states provide their own implementations for state specific methods. They may also store backreference to the context. State can then issue changes to the state of the context.
4. Both context and state can set the next state of the context.