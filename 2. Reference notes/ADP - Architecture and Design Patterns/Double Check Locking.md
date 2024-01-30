- A software design pattern used to reduce the overhead of acquiring a lock by first testing the locking criterion without actually acquiring the lock.
- Notably used in the context of lazy initialization in a multithreaded environment.

*Example: Thread-safe Singleton without incurring the cost of acquiring a lock every time an object requests access to the Singleton instance. Initially, the instance is checked to be null without locking; if null, a lock is obtained, and the instance is checked again to ensure it wasn't created in the meantime before creating the instance.*

```java
if (INSTANCE == null) {
	synchronized (Singleton.class) {
		if (INSTANCE == null) {
			INSTANCE = new Singleton()
		}
	}
}
```

[[Non-GoF Patterns]]