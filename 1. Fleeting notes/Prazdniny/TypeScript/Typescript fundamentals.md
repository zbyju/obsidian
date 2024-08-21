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