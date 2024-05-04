# REST
- Clean URL
- REST API design
- Semantic URL
- idempotent
- modify/dont modify state
- JSON RFC charset UTF8
- enveloping

# Microservices
- Resilience
- Scalability
- Technology independence
- Domain driven design
- Communication patterns
- Service discovery
- Complexity tradeoffs
- Observability - monitoring, logging, tracing
- Deployment
- Smaller scope - easier to follow
- Independent testing
- Future proofing
- Fault isolation
- Easier refactoring
- Micro != small

# Notifications
- notification approaches
- detection
	- comparison
	- deviation
	- trends
	- EMA
- limiting
	- cooldown
	- streak
	- clearance
	- user input

# Database
modifying state, idemptotent in context of dbs
does it make sense to read/write directly from a DB from a service that doesn't own the DB/table/collection?
- There can be a problem with caching
- If a service relies on itself being the only writer (CREATE, UPDATE, DELETE) to the database it can make certain operations easier (caching for example)
- If another service writes to the collection the cache will no longer represent a true state
- Therefore it is better to call the service to write to the DB instead of writing to it from yourself (from the perspective of another service)
- This can link to the ideas used in REST


# RabbitMQ
- work queue
- publish subscribe
- exchanges
- fanout
- routing
- binding

URL
REST
XML
JSON
API
JWT
DB
MQ
PDF
PWA
GSM
SMS
HTTP
WSN
MQTT
ETL
DRY
URI
HTTPS
SSR
CSR
SEO
HTML
CSS
SWR
YAML
CRUD
HATEOAS
IP
CI
CD
SQL





https://i.imgur.com/wqWOQff.png
https://web-frameworks-benchmark.netlify.app/result?f=elysia,express,fastify,gin,gorilla-mux,chi,fiber,httprouter,echo,fasthttp,django,flask,axum,rocket,akkahttp,play
https://web-frameworks-benchmark.netlify.app/compare?f=fiber,gin,echo,elysia,fastify,express,flask,django