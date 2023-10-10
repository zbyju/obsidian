chapter 1

functional programming =
only use pure functions

pure function = no side effects 
side effects = if it does something other than return a result (modifying a variable, data structure, setting a field object, throwing an exception, halting with an error, printing to a console, reading/writing to a file, drawing on a screen)

pure functions are easier to:
test, parallelize, generalize, reason about, less prone to bugs

pure function is a function f with input of type A and output of type B (f: A -> B). There can't be anything else that the function does that's observable outside the function itself.

it can also be defined using the concept of referential transparency (RT) which is a property of expressions. This property means that the expression can be replaced by the result of the expression and nothing would change.

Function is pure if calling it with RT arguments is also RT.

Expression E is RT if for all programs pp, all occurences of e in p can be replaced by the result of evaluating e without affecting the meaning of p. 

A function is pure if the expression f(x) is RT for all x that are RT.

The substitution model helps for recognizing if an expression is RTc

Tail recursion
A call is in a tail position if the caller does nothing other than return the value of the recursive call.
rec(x, y) is in a tail position
1 + rec(x, y) is not in a tail position, there is still work to be done
we can use @annotation.tailrec for the compiler to check this for us

monomorphic vs polymorphic
mono = jeden typ dat 
polymorphic = jedna funkce na vice typu
