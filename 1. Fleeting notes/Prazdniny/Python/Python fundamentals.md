# Useful functions
- `type(var)` - returns the type of the variable
- `dir(var)` - returns the methods on that variable
- `help(type/method)` - returns a help message about a type or a method

# PEP8
Coding style convention to follow when writing python code.

- 4 spaces
- Writing variables and functions lower_case

# Variables
Python is dynamically typed:

- int
- float
- complex
- str

To cast to a different type we can use the name of the type to cast to `int(), float(), ...`

### str
We can either use `""` or `''` or to make a multiline string: `"""long string"""` or a formatted string `f"Hello, {name}"`

## Functions
Functions can be declared with default values, but they need to be last in the argument list.
!!! But wathc out the default value is only created once if dealing with lists and then reused:
```python
def foo(a, b = []):
	b.append(a)
	print(b)

foo(1) # [1]
foo(2) # [1, 2]
```
Only use default values with primitive values as they are recreated every time.

Functions can be called with arguments on the positions as declared in the function declaration or with any order by specifying the name of the argument (`addNums(x=10, y=20)`)

All the variables from within the scope of the function gets deleted on the function return