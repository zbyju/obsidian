# Types / Coercion
## Primitive types
- undefined
- string
- number
- boolean
- object
- symbol
weirder
- null (subtype of object)
- function (subtype of object)
- array (subtype of object)

we can use `typeof` to get the string name of the type (primitive)

#### NaN
= Not a Number, very misleading name.

"hi" is not a NaN! even tho it's not a number

NaN symbolizes that a numeric operation went wrong; it's still a number (type is number) but the result is not a number.


### Coercion
is the operation of converting a variable from one type to another.

WE can explicitely convert to a different type using:
- `Number`
- `String`

#### Boolean coercion
Some values are **falsy** some are **truthy**, this means that when converted to a bool they will be converted to false or true.

Falsy:
- ""
- 0
- -0
- null
- undefined
- false
- NaN
- []
#### Implicit vs Explicit
Most of the time explicit conversion is better for understanding what is happening. Sometimes it can add too much noise and we can just use the implicit conversion (when using `<` for example)

### Equality
`==` allows coersion (when the types of the variables are the same then it's the same thing as using `===`)
`===` disallows coersion (can only be used on variables of the same type)

# this / prototype
this references the execution context of the call. It determines how the function was called. It is aware of the dynamic context.

we can call a function with a custom this context using `fn.call(thisArg, ...params)`

`class` can be used as a syntactic sugar for prototypes.

# Scope
Scope determines where javascript looks for variables

## undefined vs undeclared
undefined = variable that hasn't been assigned a value
undeclared = variable that has never been declared (doesn't exist)