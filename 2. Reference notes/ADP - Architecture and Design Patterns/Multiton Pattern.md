- A variation of the Singleton pattern, the Multiton pattern ensures a class has only a limited set of instances, each identified by a unique key.
- Instances are stored in a map or similar data structure, and can be retrieved based on their keys.

*Example: Game: we need exactly nine knights, each with unique characteristics. The Multiton pattern can be used to create and manage these knights. Each knight is accessed using a unique key (e.g., their name or ID), ensuring that only nine knights exist at any given time and can be easily accessed and managed.*