Publishers categorize published messages. Subscribers express interests in categories. Subscribers then receive messages from interested categories without knowledge of publishers.

- Subscribers receive just a fraction of messages
- Process of selecting messages is called *filtering*

They use [[Asynchronous Messaging]] techniques.

# Implementation
## Topologies
### Bus/Broker
- Messages sent to message broker or event bus
- Subscribers register for topics with broker
- Broker performs filtering and routing
- Broker may do additional work - message prioritization, etc.
### Data Distribution Service (DDS)
- All publishers and subscribers share data about each other using IP multicast
- Publishers and subscribers cache this information and route messages based on the discovery

## Filtering
### Topic Based
- Messages are published to topics (named channels)
- Publisher is responsible for defining that and then using it
- Subscriber receive messages based on topics they subscribed to
- All subscribers to a topic receive the same messages
## Content Based
- Messages are delivered to a subscriber if the content matches constraints by the subscriber
- Subscriber is responsible for defining that
### Hybrid
- Some systems support both at the same time

## Registration time
### Build time
- Subscriber are coded in
- Example: Click of button in GUI systems
### Initialization time
- During system initialization it connects and subscribes
### Runtime
- Based on some trigger

[[Architectures]]