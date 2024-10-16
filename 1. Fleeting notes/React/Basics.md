
# Component
Component = reusable UI element

## Defining a component
### Functional component
They are regular functions that return JSX. There can be multiple in a single file, but they can't be nested.


```js
export default function Component() {
	return (
		// JSX	
	)
}
```

1. The function needs to return JSX
2. The function needs to be exported

## Using a component
```jsx
<Component />
```

# JSX
Follows the syntax of HTML, but:
1. Can only have one root element
	- If we need more than one root then return either `<div>` or `<></>` fragment
	- This limitation is because under the hood 
2. All tags must be closed
	- No self closing tags (eg. `<img>` must be `<img />`)
3. camelCase for attributes
	- Including css properties inside style attributes
	- eg. `stroke-width` becomes `strokeWidth`
	- `class` becomes `className` because class is a reserved keywords in JS
	- ! `aria-` and `data-` are written as in HTML (for historic reasons)
## Using JavaScript
Variables can be embedded into JSX using `{variable}`. They act as a window into the JavaScript world. They can be used in 2 places:
1. Inside a JSX tag: `<h1>{ name }</h1>`
2. Inside attributes: `<img src={ avatar } />`

### Props
Components take attributes also called props. The default HTML components have attributes predefined; React components can use Props based on their function definition. Props are immutable but can change over time; this causes the component to re-render.
```jsx
export default function Component(props) {...}
export default function Component({...}) {...}

export default function Component({propWithDefault = 10}) {...}


<Component prop1={ value1 } prop2="This is prop2" />
```
#### Forwarding props
If we need to forward props to another component we can do that using the spread operator `{...props}`.
```jsx
export default function Component1(props) {
	<Component2 {...props} />
}
export default function Component2({...}) {...}
```
### Components as children
There is a special prop called `children` that receives the JSX that's put inside the component.

```jsx
export default function Component1(props) {
	<Component2><h1>Hello</h1></Component2>
}
export default function Component2({children}) {
	<div>
		// ...
		<div class="heading">{children}</div>
		// ...
	</div>
}
```

This allows us to wrap some HTML around the children or put the children in a specific place in the tree.
### Conditional Rendering
1. Using if to return different things
	- Useful when returning completely different JSX
```jsx
if(bool) { return (/* JSX1 */)}

return (
	// otherwise return this
)
```
2. Using ternary
	- Useful when we have different things inside our JSX to return
```jsx
return (
	<h1>{bool ? "Hi" : "Hello"}</h1>
)
```
3. Using AND
	- Useful when we want to render something only when a condition is met
	- Don't put numbers on the left side (0 == false)
```jsx
return (
	<h1>{ bool && "Is True"}</h1>
)
```
4. JSX in a variable
	- Useful for extracting parts of JSX outside for readability
```jsx
let name = <span>John</span>

if (isJames) {
	name = <span>James</span>
}

return (
	<h1>{ name }</h1>
)
```
5. Using OR
	- Similar to AND but for different conditions
```jsx
return (
	<h1>{ bool || "Empty"}</h1>
)
```

If we want to return nothing then we return `null`.

### Rendering lists
1. Define a list as an array
2. Map the array into a JSX
```jsx
const jsx = list.map(item => (<li>{item}</li>))
```
3. Output the result:
```jsx
return (
	<ul>{jsx}</ul>
)
```
4. Define the key of the item
#### Filter lists
We can additionally filter lists using `filter` method.
#### Key
It tells react which component corresponds to each item in the array. When the array is modified react can then track which items are where in the DOM.

Rules:
- They must be unique among siblings
- They must not change

Where to get them:
- ID from a database
- Locally generated (eg. using UUID); these must be persistent over re-renders.
### Pure functions
- It doesn't effect anything outside its scope.
- It gives the same output for the same inputs.

We should strive for having our components pure - they should take props and based on them produce the same JSX each time without effecting other components.

## Render Tree
The application and its components are represented as a tree with a single root. There is a root component which renders other components which form a tree.

A render tree represents a single render pass; due to data changing and conditional rendering, the render tree might change over time.

They are important for performance optimizations. Top-level components are closer to the root and cause re-rendering in child components, which cause performance issues. Leaf components are near the bottom and are often re-rendered due to their parents being re-rendered.
### Dependency trees
They represent the relations between modules (imports). They allow build tools to bundle only necessary parts of the code and for debugging.

They are often similar to render trees.
