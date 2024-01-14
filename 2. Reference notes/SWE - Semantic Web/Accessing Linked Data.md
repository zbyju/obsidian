There are 2 strategies for accessing linked data:
- Direct dereferencing
- 303 URI Strategy

# Basic Strategy of Dereferencing URIs
1. Client dereferences URI and sends HTTP request
2. Service gets the request and sends back the requested resource
3. Client interprets the data

![https://i.imgur.com/U8vHp7D.png](https://i.imgur.com/U8vHp7D.png)

# 303 Strategy for Dereferencing URIs

1. Client send HTTP GET request to the URI of a resource
2. Server returns HTTP 303 See Other (redirect) with URI to a document describing the resource
3. Client performs HTTP GET on the URI returned by the server
4. Server sends back the data

## Advantages:
- Clear distinction of the entity and the document describing it
- Allows for better content negotiation


[[_SWE Reference]]
[[Linked Data]]