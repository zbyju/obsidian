**Mashup aplikace, pravidla same-origin policy. Protokoly CORS, JSONP, JWT.**

# Mashup application
Applications that combine data from multiple sources/APIs:
- Data Mashup - data integration/aggregation only (read only)
- Service Mashup - More sophisticated (read, write)
- Visualization - involes UI more

- Client-side mashup (in browser)
- Server-side mashup - server side integration

# Same Origin Policy
Browser can make requests only on the same domain (host, port)

There are 2 solution for this problem.

This is to prevent attacks:
- XSS (Cross-site scripting) attacks - injecting javascript to a website and then running a script utilizing the cookies and sessions the user has stored.
- CSRF (Cross-Site Request) attacks - injecting content to a website, when it loads it sends requests to another website to retrieve data
# CORS
![[Pasted image 20240516163718.png]]
There is a preflight request using OPTION method (automatically for each request by browser), this is then cached.
If the preflight is accepted by the server according to the Access-Control-Allow-Origin, -Method, -Headers then the actual requested is made.
# JSONP
It’s a technique to overcome Same-Origin Policy that would normally block the request.

1. We have a function 
```js
function handleResponse(data) { console.log(data); }
```
2. And we create a script tag and use its src attribute to access the JSONP endpoint. The src attribute is not checked with SOP.
3. The server responds with: 
```js
handleResponse({
  "name": "John Doe",
  "age": 30
});
```
This can be a workaround the same origin policy, but we can only make GET requests.
# JWT
Mechanism to securely transmit information between parties as a JSON object.
Can be verified, trusted; it is compact and self-contained. The structure is:
`<header>.<payload>.<signature>`
## Header
Contains 2 parts: type of token and algorithm used (HMAC, SH256, RSA)
## Payload
Contains the claims (statements about the entity - user)
## Signature
Signed encoded header, encoded payload and a secret

The whole JWT is then encoded using BASE64
