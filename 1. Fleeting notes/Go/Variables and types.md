# Declaration
```go
var username string = "user"
fmt.Println(username)
fmt.Println("Variable type is: %T \n", username)

var isLoggedIn bool = false // default: false
var smallVal uint8 = 255 // default: 0
var unsigned uint = 1234 // default: 0
var signed int = -1234 //default: 0

var smallFloat float32 = 1234.1234
var float float64 = 12341243.12341234

// default value
var anotherVariable int // 0

// implicit
var str = "this is going to be a string"
```

# Declaration with initialization
```go
username := "user"
```

You can only use that inside a method
Can't use it for global variables

# Public
If we want to use variables or function outside our file (package) we need to make it capital
```go
var Username = "test"
```

# Const
We can make a variable constant by using `const`

```go
const PI = 3.14
```