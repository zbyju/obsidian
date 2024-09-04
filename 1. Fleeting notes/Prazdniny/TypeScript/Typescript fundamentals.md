# TSConfig
```json
{
	compilerOptions: {
		outDir: "path where to build the project",
		target: "version of the output (e.g. ES2015)",
		moduleResolution: "how to resolve imports (e.g. node)"
	}
	include: ["what are we compiling", "all the folders"]
}
```
# Type system
We can think about the type of a variable as a set. Each variable has a set of types of which it can be.

Literal type is a type that has only one value (`const x = 10 as const` - x can only be 10)

When we assign a value to a variable (reassign) typescript checks if the value is inside the set of types of that variable.

If typescript can't figure out the type it assigns the type `any` - this is called implicit any.

We can cast a variable to a different type using `const x = 10 as number`. This can only be done if the type we are casting from is a subset of the type we are casting to (`let x = "nope" as number` wouldn't work)


## Functions
Function arguments are denoted using `(arg: type, arg2: type2, ...)` and the return type is denoted after the arguments `(...): returnType { ... }`

Typescript will figure out the return type. If we don't specify the type it will figure it out and we get errors when callign the function when we treat the return value differently. On the other hand if we explicitly state the return type we don't get the errors when calling the function but in the function declaration if we try to return a different type.

If we have a function that should have a very clear interface that shouldn't change then we should use explicit return type. If the function's return type is a bit more loose we should use the implicit return type and let the consumers of the function figure out how to handle it.

### Objects
We can declare object types: `let obj: { key1: string; key2?: number; ... } = { key1 = "str", key2 = 2 }`. We can also say that some properties are optional using the `?` after the name of the field.

We can do a "dictionary" object:
```ts
const dict: {
	[k: string]: number
}
const dict2: {
	count1: number;
	[k: string]: number
}
```
These objects can have as many fields as they want but all have to have type number. Dict2 provides better code hints because typescirpt knows that at least count1 has to exist on the dictionary.

### Arrays
Any type can be turned into an array by putting `[]` behind it.

We can tell typescript to treat an array as immutable by using the `readonly` keyword:
```ts
const immutableArray: readonly string[] = ["hi", "hello"]
```

### Tuples
For tuples we need to explicitely say the type otherwise typescript just assumes we are declaring a normal array:
```ts
let myCar: [number, string, string] = [2002, "Toyota", "Corolla"]
```

## Nominal vs Structural Types
Typescript doens't check if two types are equivalent (the same) it asks if one type is a subset of the other.

### Static vs Dynamic
It deals with when type checking is done
Static is done during compile time (Typescript, C#, Java, C++, Haskell, Scala)
Dynamic is done during runtime (Javascript, Python, Ruby, PHP)

### Duck typing
If it looks like a duck, swims like a duck and quacks like a duck then it's probably a duck.

If the functionality is there typescript doesn't care that there is some extra stuff, it fill fit.

### Strong vs weak types
There is no real definition of this - it usually just means static vs dynamic

### Nominal vs Structural
Nominal cares about the name (being an instance of something) of the type. If i have a function that accepts class Car and pass it some object it will check if that object is indeed a Car (or a child of Car - inherits)

Structural doesn't care about what instance the variable is, what matters is that it is compatible structurally with the type we are checking against.

## Union and intersection
Again we think about types as sets => we can do set operations. Combine types using union (`type1 | type2`) to allow either of types and interect to create a type that needs to satisfy both types (`type1 & type2`) 

Usually we as a user use the union type more. Typescript on the other hand needs to be more careful and uses intersection more - when returning from a function a union type, typescript allows us to only access the properties that are on the intersect of the types.

We can narrow these types down using type guards. These are just conditional checks that narrow down the type.

### Narrowing a type
When we use a union type we might need to check what the actual type of the variable is at runtime. We can use type guards.

#### Type guards
1. Using instanceof to check the class of the variable
```ts
if(var instanceof Error) {
	return "Err"
} else {
	return "Ok"
}
```
2. Discriminated union
```ts
const [type, value] = someFun() // type is "error" | "success", then value either contains error or the value depending on the type

if(type === "error") {
	return "Err"
} else {
	return value // We know that value can't be an error
}
```
This can be only used when the discriminator uniquely identifies the type of the value.

## Defining types
We can either use type alias, which can be used to give a name to any type; or an interface that defined an object.


### Type alias
```ts
type Amount = {
	value: number;
	currency: string;
} | Error

function fun(): Amount // <- we can use the name of the type instead of using the type itself.
```

### Interface
Interfaces describe properties of an object. We can't use union or intersection, but we can work in a more OOP style (using extends from other interfaces). 

```ts
interface Amount2 {
	value: number | null; // This is Ok
	currency: string;

	toString(): string;
} // Can't do a union here.
```

Interfaces are open, type aliases are not:
Interfaces can be redaclared to change what they describe, type aliases cannot.

This means that if we have 2 interfaces that are "overriding" each other they are actually gonna be treated as one interface that is extended by all the interfaces.
```ts
interface Test {
	field: string;	
}

interface Test {
	year: number;
}

let obj: Test // { field: string, year: number }
```
#### Data type registry
This can be great for creating an extensible data type registry.

We can use the `declare module` directive that essentially injects the types specified within that block into another file to extend it.
```ts
// ------ My central library that doesn't know how it's gonna be used
export interface DataTypeRegistry {
	// Empty on purpose
}

export function fetchRecord(arg: keyof DataTypeRegistry) {
	// Implementation
}

// ----- Other code somewhere else in the codebase that extends my code
export class Book {
	// Implementation
}
declare module "/path/to/my/library/registry" {
	export interface DataTypeRegistry {
		book: Book
	}
}

// ----- Another code somewhere else in the codebase that extends my code
export class Magazine {
	// Implementation
}
declare module "/path/to/my/library/registry" {
	export interface DataTypeRegistry {
		magazine: Magazine
	}
}

// Now DataTypeRegistry is = { book: Book, magazine: Magazine }
```

#### Extends and implements
When inheriting from the same 'type' of a thing (class from class, interface from interface) we use `extends`. When we inherit from an interface we use `implements`.

## Recursive types
```ts
type NestedNumbers = number | NestedNumbers[]

const val: NestedNumbers = [3, 4, [1, 2, [5], 6], 7]; 
```

## Type query
They are used for extracting type from an existing variable

### keyof
It allows extracting type from an object by making a union type of all the keys the object has

```ts
const obj = {
	1: "hi",
	"field": 123
}
type keys = keyof obj // 1 | "field"
```

### typeof
It allows us to get a type from a variable.

```ts
const x = someFun()

type typeOfXIs = typeof x // Will have the actual type that someFun returns.
```

This keyword can be used within a condition too, but then it can't be used to identify an object as it returns `"object"` for all objects. It can only be used to differentiate between primitive values.

```ts
const obj = { field: 123 }
if(typeof obj === "string") return "It's a string"
if(typeof obj === "object") return "It's a object" // Can only be used to differentiate primitive types
```

### Combining keyof and typeof
When we want to get the type representing the possible keys in an object from a value (if we wanted to get it from a type we could use `keyof` directly), we can combine keyof and typeof.

First get the type using `typeof` and then we can use `keyof` because we are already working with a type.

```ts
const obj = {
	name: "hi",
	year: 1234
}
type IWant = "name" | "year"
type Solution = keyof typeof obj
```
### Indexed Access types
We can get the type of a field of an object.

```ts
interface Obj {
	field: number;
	year: number;
	color: string
	fieldObj: {
		name: string;
		fieldNested: {
			x: number
		}
	}
}
type fieldObj = Obj["fieldObj"] // { name: string, fieldNested: { x: number }}
type fieldNested = Obj["fieldObj"]["fieldNested"] //  { x: number }

type fieldUnion = Obj["year" | "color"] //  number | string
```
#### Union type through index
We can also use union within the index access to get the union of the individual fields.

## Callables
They are types that hold a type of a function.

```ts
type Adder = (x: number, y: number) => number

// Or even with interface
interface Adder2 {
	(x: number, y: number): number
}
```

### void
`void` is a type that we can use to say that we don't care about the value that a function returns.

A function that returns nothing actually returns `undefined` but typescript treats this scenario as the function returning `void`.

`void` and `undefined` are not the same though, `void` says that the value the function returns doesn't matter as it will not be used, `undefined` says that it actually expects `undefined` to be returned from the function (by either returning `undefined` or not returning anything).

```ts
function fun1(cb: () => undefined) {
	// Impl
}
function fun2(cb: () => void) {
	// Impl
}

fun1(() => 2) // This will give an error as typescript is expecting undefined but gets a number
fun1(() => 3) // This will be okay because typescript doesn't care what the return value of the callback is
```

### Constructables
Constructables are for defining types that are able to be called with the `new` keyword.

```ts
interface MyClass {
	new(value: number): Date
}
```

### Function overloading
If a function has multiple parameter types that it accepts but they depend on each other then we can define multiple function heads to tell typescript what combinations are allowed.

```ts
function fun(type: "string", value: string): string 
function fun(type: "number", value: number): number
// Function either gets type = "string" and then all the rest of the values are also string, or type = "number" and then all the values are numbers
function fun(type: "string" | "number", value: string | number): string | number {
	// Implementation
}
```

The actual function still needs to be typed. Typescript only checks that the heads match what the main function sets as the types, but not the other way around. If we want to kinda infer types from the heads to the main function then we can type everything as `any`.

### this
If we want to type the `this` to have a correct type we can add it as parameter to our function; the function will still have the same amount of parameters, but it's a place where we can tell typescript what the type should be.

The parameter actually has to be called `this` otherwise it will be treated as a normal parameter.