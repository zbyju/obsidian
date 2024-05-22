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
	- CGroup (Control Group)
### Mount
- File systems in the global namespace are visible to all namespaces
- File systems in other namespaces are not visible to the rest of the system