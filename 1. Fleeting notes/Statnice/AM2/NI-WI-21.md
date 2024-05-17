**Bezpečnost na webu, protokoly OAuth a OpenID, protokol TLS. Protokoly pro realtime web (SSE a WebSocket).**

# Concepts
- Authentication - verify client identity
- Authorization - verify rights to access resources
- Message Confidentiality - keep message content secret
- Message Integrity - keep message content unchanged
- Non-repudiation - proof of integrity and origin of the data
# Authentication
## Basic
`username:password` base64 encoded
The password can be read, operations can be repeated
# Digest
- No password between client and server, hash value instead
- No repeat operations because of using nonce value
1. Client accesses protected endpoint
2. Server asks for authentication using WWW-Authenticate which specifies information + nonce (limited lifespan)
3. Client calculates the hash based on username, password and nonce and sends them in Authorization

# TLS
TLS is an upgrade over SSL. It sits on the session level (in TCP/IP)
Peers must agree on ciphersuite and keys, which is achieved in the TLS handshake. Every message is signed using MAC

## TLS Handshake
0. First there is the classic TCP handshake (1RTT)
1. ClientHello - TLS protocol version, list of ciphersuites, TLS options
2. ServerHello, Chooses version, ciphersuite; sends certificate
3. RSA or Diffie-Hellman key exchange
4. Message integrity checks; sends encrypted Finished
5. Decrypts the message and gets ready to receive data
6. Sends data
7. Receives data
Takes 2 RTT (overall 3RTT with TCP handshake)
## Proxy Servers
- Offloading
	- Inbound TLS, outbound normal
	- Proxy can inspect messages
- Bridging
	- Inbound TLS, outbound a new TLS connection
	- Proxy can inspect messages
- End-to-end TLS (pass-through)
	- TLS connection is passed through the proxy
	- Proxy cannot inspect messages
- Load Balancer
	- Can use TLS offloading or bridging
	- Can use TLS pass-through with the help of Server Name Indication (SNI)
		- SNI - ClientHello includes the hostname the client wants to communicate with

# OAuth
Mechanism for users to grant access to third party apps without exposing their credentials
![[Pasted image 20240516183858.png]]

## Terminology
- Client - third party app accessing resources owned by resource owner
- Resources Owner (user) - person owning data on resources server
- Authorization and Token Endpoints - provided by authorization server through which 
- Resource Server - application that has the data (Google Calendar)
- Authorization Code - a code the client uses to request access tokens
- Access Token - a code the client uses to access the resources
## Client-Side
![[Pasted image 20240516211652.png]]
1. Client application redirects the user to the authorization endpoint
2. They review the action
3. Auth server informs the resource server
4. Auth server redirects the user back to the application with the access token
5. User extracts token
6. User can use the token to retrieve data from resource server (for the specified time)

## Server-side
![[Pasted image 20240516212040.png]]
First 4 steps are the same (retrieving the access token)
5. Client then requests the access token and refresh token from a different endpoint based on the provided authorization code.
6. Client makes request with the obtained access and refresh tokens

# OpenID
![[Pasted image 20240516213446.png]]
1. Login form
2. User clicks on a provider
3. Web application does a discovery of the openid provider
4. It gets a XRDS - it provides some information (endpoint)
5. The application sends a request to the provider
6. User gets redirected to the provider
7. User logs in + grants permissions
8. The application gets the information it needs and the user is redirected back to it
9. User can access

# Server Sent Events
Standard HTTP is used to push events. The client listens, the server sends data with type: `text/event-stream`.  The data is sent in the body of the response with each line having `data:...\n`. The last line has two newlines `\n\n`. There can also be `id:` to provide an id to the message.

It offers reconnect, the browser does it automatically + can provide information about the last seen message.

It is simple, real-time communication, auto-reconnecting, but only one way communication.
# WebSocket
Realtime protocol on top TCP which supports bi-directional communication.

The connection is established either over TLS or by having a HTTP/1.1 connection and then upgrading to websockets. Server responds with 101 Switching protocols.

The communication is now done using the TCP socket and WebSocket protocol without overhead of HTTP; each websocket connection requires its own tcp socket. The communication is done in frames, each has headers: length, closing frame, type of data and then payload. Each message is made out of 1 or more frames (application on client and server are not aware of framing).

Large messages can cause head of line blocking, therefore its good to split messages into smaller ones.

The socket might get closed, we need a backup strategy.