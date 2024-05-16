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
Users