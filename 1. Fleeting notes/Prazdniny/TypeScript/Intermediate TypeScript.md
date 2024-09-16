# Declaration Merging
Identifiers are what we can export from a file. These can be:
- variable
- interface/type
- namespace

We can define any of these three on an identifier. This means that a single identifier can contain a value, a type, or a namespace or a combination of these.

Declaration Merging says what things are "riding" on a single identifier.

```ts
const my_identifier = "value"
type my_identifier = number
namespace my_identifier {
	// ...
}
```
## Rules
Type: can't be used as a value
Value: can't be used as a type
Namespace: can be used a value; cant' be used as a type
## Namespace
It is used for weird edge cases where we need to type something but on top of that we need to add more functionality.

Namespace is kind of like a value, as it is used to define further functionality to the value.

```ts
function fun(str: string): number {
	return Number(str)
}
namespace fun {
	export function other(x: number): string {
		return x + "!"
	}
}
// Now we can use:
fun("hi)
fun.other(10)
```
## Class
Class can be used as a value
Class can be used as a type

Class uses declaration merging for a value and a type at the same time.
# Top and Bottom types
## any
It is a top type => accepts anything
Basically disables typescript.

It is not evil to use. Sometimes it is the best type to use.

If a function can accept anything and still work then we should use any (e.g. `console.log` accepts anything so it should have `any` in its declaration).
## unknown
It is a top type => accepts anything
Before we use the variable we need to narrow down what type the variable is.

The difference between `any` is that typescript won't let us unit if we don't narrow it down.
## object
Almost top type => accepts anything but primitives
## {}
Almost top type => it accepts anything but `undefined` and `null`

It can be used to remove nullability from a type using `&` the intersection.
## never
Bottom type => no variable can be of this type
It represents an empty set

```ts
type Vehicle = Truck | Car // Later on: | Boat

if(vehicle instanceof Truck) {

} else if(vehicle instanceof Car) {

} else {
	const x: never = vehicle; // This will tell typescript that this an exhaustive check and we should never get here. If vehicle type changes we get a type error here.
}
```
## void
Almost bottom type => it represents a return type of a function that doesn't return anything

It accepts unknown.

# Nullish values
## null vs undefined
null is something that has to be said
undefined is something that might've never been said

If we have an optional field and never set it, it is undefined.
Null has to be explicitly set.
## non-null assertion operator
We can use `!` to indicate that we know that at this point the value is not nullish.

It is not safe to use.

It is useful for tests, we want tests to fail.
## Optional chaining
If we have optional fields in objects and we want to either safely get the value or get undefined with the first undefined field.

```ts
return object?.optional?.field?.value

// vs 
if(object === undefined || object.optional === undefined || object.field === undefined) return undefined
return object.optional.field.value
```
## Nullish coalescing
We can use `||` to get either the value or if the value is falsy then we get the other value.
When the value can be falsy (0, "") but we want it to remain then we can use `??` that only works with nullish values.

```ts
const x: 0 | 50 | 100 | undefined = 0
const y = x || 50; // Here y will be 50 when x was 0
const z = z ?? 50; // Here the fallback will be used only with undefined
```
# Modules & CJS interop
# Generics Scopes and Contraints
# Conditional Types
# Inference with conditional types
# Mapped types
# Type registry
# Variance over type params