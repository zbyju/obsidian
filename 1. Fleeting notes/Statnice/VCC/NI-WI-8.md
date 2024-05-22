**Principy kontejnerizace, aplikační vs. systémové kontejnery, princip, druhy a typy jmenných prostorů (namespaces), princip a význam řídících skupin (cgroups), vrstvený souborový systém v Dockeru.**

# Containerization
**Container** = form of virtualization which relies on separating kernel resources. It is easier than classical virtualization because it shares the kernel and therefore it is easier to share the memory and disk.

They use Linux features to do that:
- Namespaces
- CGroups
- Seccomp
- SELinux
## Namespaces
Namespaces are functions of the kernel which can separate kernel resources such that one set of processes sees one set of resources and other processes a different set of resources.
- Resources can exist in different namespaces
- After system starts there is only one namespace for each type; processes can then create namespaces and become their members.
- The namespace dies when there is no process inside it + noone holds its descriptor
- There are 8 types of namespaces:
	- Mount
	- UTS (Unix Time Sharing)
	- IPC (InterProcess Communication)
	- PID (Process ID)
	- Network
	- User
	- Time
### Mount
- File systems in the global namespace are visible to all namespaces
- File systems in other namespaces are not visible to the rest of the system
### UTS
Separating name of the system between real computer and containers. It changes the hostname and domain.
### IPC
Separating resources for interprocess communication - segments of shared memory, semaphores, queues of messages.
### PID
Isolation of the list of processes in containers. Parent namespace sees all processes but child namespace doesn't see parent processes. Child namespace has their own numbering of processes starting from 1 again (important for system containers).
### Network
Virtualizes the network queue. When namespace is created there is only loopback. Each network device exists in only 1 namespace. Each namespace has its own IP addresses, routing table, list of opened sockets, firewall, ...
### User
Separates the mappings of username -> UID and isolates permissions. We can have a user inside the namespace with UID 0 (root) but outside he might have normal user privileges.
### Time
Allows for different systems times to exist (timezones).
## CGroups
Namespace give a way of separating resources; Control Groups give a way of separating the amounts of resources. They use controllers.
### CPU
CPU CGroups controllers have access to the scheduler and directly influence it.
- Each group has a share of the CPU assign to it.
- They also throttle CPU by assigning how much time per 1s they can use
	- This is done by token bucket - there is $r$ tokens/sec coming in and the bucket can hold up to $b$ tokens (for burst when more power then r/s is needed).
### Memory
Limits how much each group can use of the main memory.

Low amount of memory leads to swaps and I/O operations that slow down the whole system.
### I/O
- Limiting access to devices - read, write, create.
- Prioritizing access to I/O among groups and also to network interfaces.
# Docker
## Layer Filesystem
The format of image distribution optimizes the amount of transferred data aggressively.

It doesn't create layers on block layer, it does so on file level. If there is a file change between layers, then the whole file gets saved/transferred.

When container is started, topmost layer is created and opened for writing; another layer can be created from it.

The final layer is deleted when the container is deleted. 

When running the container the layers are merged together (union file system). There are different drivers for implementing the layered filesystem.
One approach is to read from the lowest (most recent) layer; when writing it is copied to a new layer where it is modified. Deleting is done by creating a new layer that whiteouts the file (flags as deleted).

The advantage of layered filesystem is caching. If we have some layer donwloaded, we don't need to download it again.

Image of the container has:
- Manifest - metadata about dependencies, hashes of each layer
- Layers - tar.gz
- Configuration - name of application, arguments, environment variables

DockerHub has repositories of images.
## Running Docker
Docker daemon listens for API calls on terminal.
It runs the containers = runs it + creates 1 more layer for writing
## Dockerfile
1. Specify image from which to start
2. Then there are commands for building the container
3. Finally there is a command for running the application and its arguments

Each line of the dockerfile is one layer.
## Volume
They are a directory in a filesystem; they are removed from the layered system:
- Higher performance (no need to use the layered system) - good for read heavy
- Persistence - It survives deleting the container and can be used with another container; they can even be connected to multiple containers at the same time
## Network
### Bridge
By default containers are in their own network namespace and then are connected using a virtual bridge together using the *bridge* driver.

They can access internet using NAT, but are no accessible from the outside. Between themselves they can be addressed by their name; or by IP.

Services are made available using port forwarding.
### Host
We can also run privileged containers that have access to the host's network adapters using *host* driver.

This driver doesn't create a network namespace and all services are directly accessible.
## Logging
Services should not log into /var/log (creates new layers) and we would lose logs when container is deleted.

Docker daemon listens on stdout and stderr and save the logs.
We can also log directly to API or database
We can also log into a volume.