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
mux.HandleFunc("/edit, )
```