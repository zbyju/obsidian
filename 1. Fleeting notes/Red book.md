chapter 1

functional programming =
only use pure functions

pure function = no side effects 
side effects = if it does something other than return a result (modifying a variable, data structure, setting a field object, throwing an exception, halting with an error, printing to a console, reading/writing to a file, drawing on a screen)

pure functions are easier to:
test, parallelize, generalize, reason about, less prone to bugs

pure function is a function f with input of type A and output of type B (f: A -> B). There can't be anything else that the function does that's observable outside the function itself.

it can also be defined using 
