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