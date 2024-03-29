To create a new go project we have to choose a unique identifier for the project and then run:
```sh
go mod init PROJECT_ID
```

To run the project we can use:

```sh
go run .
go run main.go
```

# Working with net/http

It is part of the standard library for building web applications

## Create a new server
1. Create a serve mux:
```go
mux := http.NewServeMux()
```
2. Register routes (mapping between route and handler)
```go
mux.HandleFunc("/", home)
mux.HandleFunc("/user/", userView)
```
3. Make handlers
```go
func home(w http.ResponseWriter, r *http.Request) {
	w.Write([]byte("Hello from home"))
}

func userView(w http.ResponseWriter, r *http.Request) {
	w.Write([]byte("User view page"))
}
```
4. Listen on port
```go
log.Print("Starting on port 4000")
err := http.ListenAndServe(":4000", mux)
log.Fatal(err)
```

`/` route is a catch all route; to fix that we can:

```go
func home(w http.ResponseWriter, r *http.Request) {
	if r.URL.Path != "/" {
		http.NotFound(w, r)
		return
	}
	w.Write([]byte("Hello from home"))
}
```

To access the URL path as a string we can use `r.URL.Path`.

In serve mux longer URL paths take precedence.

Request URL paths are automatically sanitized. If a user sends `/foo/bar/..//./baz` they will get redirected to `/foo/baz`, because:
- `..` is go up a level
- `.` is stay at the level
- ` ` stay at the level

Users are automatically redirected if they are missing a trailing `/` (`/foo -> /foo/`)

## Default servemux
Instead of using `mux := http.NewServeMux()` we can use a default serve mux stored in a global variable inside `net/http`.

```go
http.HandleFunc("/", home)
// ...
err := http.ListenAndServe(":4000", nil) 
```

This approach makes things a tiny bit simpler, but it's not good for production applications. It uses a global variable that can be exploited.

## HTTP Status code
We can return a different status code by using `w.WriteHeader(statusCode)` (for example `w.WriteHeader(405))`.

This can only be done once. If you call the WriteHeader method after calling Write or another WriteHeader it will have no effect.

## Helper
We can also use a helper function to do that for us:
```go
http.Error(w, "Method not allowed", 405)
return
```

This will take the ResponseWriter and use it to return the data (text) containing `Method not allowed"` with status code 405.

## Constants
```go
http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
return
```

The net/http package has all sorts of constants for different status codes. This makes the code easier to read (especially when using status codes that are not as common)

## Automatic headers
Go sets some headers automatically:
- Date
- Content-Length
- Content-Type
	- This doesnt automatically detect JSON and will send it as plain text
	- To fix this: `w.Header().Set("Content-Type", "application/json")`

## Header manipulation
We can use `w.Header()` to access the Map that holds the headers and change them using:
- `.Set(key, value)` - Adds/overwrites header to new value
- `.Add(key, value)` - Adds/appends new headers (creates multiples) to new values
- `.Del(key)` - Deletes header
- `.Get(key)` - Gets the first header
- `.Values(key)` - Gets all the headers

The header name will always get canonicalized (first letters are upper case).

## Query parameters
We can use `r.URL.Query()` to get the Map that holds the parameters and then use methods to access them:
- `.Get(key)` - to get the query parameters based on its name

# Code structure

Good code structure can be:
- **cmd** - folder that contains application specific stuff (main, handlers etc)
- **internal** - folder that contains application non-specific stuff (validators, sql models)
- **ui** - folder that holds assets such as html, css and other non-go stuff
## Internal
It carries a specific meaning in go - packages inside this folder can only be imported by the parent of this folder. In our case we can import them from our project but not other. 

This is good because we know that noone is relying on this code and can be sure that we can change it.

# Templates
Go provides `html/template` package that contains functions for parsing and rerendering html files.

```go
ts, err := template.ParseFiles("./ui/html/pages/home.tmpl")
if err != nil {
	log.Print(err.Error())
	http.Error(w, "Internal Server Error", 500)
}

err = ts.Execute(w, nil)
if err != nil {
	log.Print(err.Error())
	http.Error(w, "Internal Server Error", 500)
}
```

1. `.ParseFiles(path)` - parses the file into a template set
2. `.Execute(w, data)` - returns the html to the client and adds data to it

## Serving static files
We can use `net/http` that comes with a `http.FileServer`.

```go
fileServer := http.FileServer(http.Dir("./ui/static/"))

mux.Handle("/static/", http.StripPrefix("/static", fileServer))
```

StripPrefix will make sure we are matching correctly on the URL as we want (now we can access using `localhost:4000/static/` and see the structure inside `/ui/static` folder).

If we want to disable folder access we have several options:
- Add empty index.html to each folder we want to disable
	- This will serve the index.html instead of showing the contents of the folder
- Make a custom implementation of a fileserver

If we wanted to serve just a single file we can make use of `http.ServeFile(w, r, path)` it doesn't automatically sanitize inputs so we can use `filepath.Clean()`.

# Handler
Handler is any object that satisfies the `http.Handler` interface:
```go
type Handler interface {
	ServeHTTP(ResponseWriter, *Request)
}
```