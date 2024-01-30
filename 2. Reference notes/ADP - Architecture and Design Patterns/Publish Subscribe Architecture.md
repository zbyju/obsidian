Publishers categorize published messages. Subscribers express interests in categories. Subscribers then receive messages from interested categories without knowledge of publishers.

- Subscribers receive just a fraction of messages
- Process of selecting messages is called *filtering*

They use [[Asynchronous Messaging]] techniques.

# Implementation
## Bus/Broker
- Messages sent to message broker or event bus
- Subscribers register for topics with broker
- Broker performs filtering and routing
- Broker may do additional work - message prioritization, etc.
## Data Distribution Service (DDS)
- All publishers and subscribers share data about each other using IP multicast
- Publishers and subscribers cache this information and route messages based on th

[[Architectures]]