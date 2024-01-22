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
1. Create server:
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
	http.Not}
	w.Write([]byte("Hello from home"))
}
```