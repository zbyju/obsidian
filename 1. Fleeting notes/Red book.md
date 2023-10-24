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

covariance of the generic type (List[+A])
for all types X, Y, if X is a subtype of Y, then List[X] is a subtype of List[Y]

how to write efficient data structures in immutable way?
they need to exploit data sharing

algrebraic data types

functional approach does not need to concern about encapsulation that much. data is immutable so outsiders can't really break something externally.

Handling errors:

problems with exceptions:
they propagate silently and you might not now that you are supposed to handle it

using special values:
sometimes there is no special value (max of Ints when the array is empty)
the caller doesn't know what to check for (what are the special values in this case)

another parameter for error values:
ask the caller to tell us what value we should assign in that case
this doesnt give us any options
