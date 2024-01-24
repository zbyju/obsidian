1. Define construction steps
	- If you can't then builder pattern is not applicable
2. Create concrete builder implementations with different construction steps
	- It needs to have all steps
	- It needs to have a special method for retrieving the result
		- This method should not be part of the abstract builder
			- The result doesn't have to share an interface
			- It only shares the construction steps
3. Consider implementing a director class with predefined construction 