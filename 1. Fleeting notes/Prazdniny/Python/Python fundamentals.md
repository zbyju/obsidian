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

# List
## Sorting
Lists can be sorted two ways:
1. return a new value
	- using `sorted(list)`
2. in-place
	- using `list.sort()`

## Adding items
1. Append
	- using `list.append(item)`
2. Insert at index
	- using `list.insert(index, item)`
3. Concating 2 lists
	- using `list.extend(other_list)`

## Item lookup
1. Is item in list
	- `item in list`
2. Finding index of an item
	- `list.index(item)`
3. Access by index
	- `list[index]`

## Removing
1. Remove item
	- `list.remove(item)`
2. Pop - remove last
	- `list.pop()`
3. Pop - remove at index
	- `list.pop(index)`

# Tuples
Lists are mutable, tuples are immutable. To make a tuple we need to use a comma (,)

`tuple_1_value = (1, )`
`tuple_2_values = ("hey", "hello")`
`comma_is_important = 1, 2, 3` - also a tuple

We can use similar functionalities to a list, but tuples are immutable, so we can't change them.

## Unpacking
We can unpack any tuple into variables:
`str1, str2 = tuple_2_values`

The number of variables always have to match the number of values in the tuple. If we don't care about one of the values then we can name it `_`.