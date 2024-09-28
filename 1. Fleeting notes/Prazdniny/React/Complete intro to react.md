React is just a library with some functions that we can use.

We can create elements using `React.createElement(name, attibutes, inner)` It takes 3 attributes:
1. name of the DOM element (e.g. `"div"`, `"my-custom-element"`)
2. attributes object (e.g. `{}`, `{ id: "my-id" }`)
	1. Classes
	2. Ids
	3. Props
3. The inner HTML of that element:
	1. Text (`"Some string ot be put inside the element"`)
	2. Another element (using React.createElement again to add another element inside)
	3. An array of elements
	4. A function that returns an element
		1. This is called a component
The last 2 arguments are optional

We can instead use JSX which is a nicer syntax that on uses createElement automatically for us.

## Hooks
We want components to render fast because they typically rerender often. We want to keep them pure and not changing anything external.

We can use hooks to make sure we are adhering to these principles.

All hooks need to be declared in the same order on each render => they can't be inside ifs, loops, ...
### useState
Hook for storing state.
### useEffect
Used for side effects.

Accepts a dependency array as second argument:
- not defined = run every rerender
- `[]` - run on first render
- `[deps]` - include all dependencies that trigger the effect being ran again
### Custom hook
We can create a custom hook that can use other hooks. It has to start with `use` in the name of the function.

Some people never call the built-in hooks directly and always wrap them inside their own hook.




