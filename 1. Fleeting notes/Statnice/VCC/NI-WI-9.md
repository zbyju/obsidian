**Cloud Computing: Definice cloudu (5 vlastností), modely nasazení, rozdíl mezi Platform-as-a-Service (PaaS) a Infrastructure-as-a-Service (IaaS), plánování v cloudu, cloudové služby pro vyvažování zátěže (load balancing), objektové, souborové a blokové datové úložiště.**

# Cloud
## Definition
1. On-demand self-service
2. Broad network access
3. Resource pooling
4. Rapid elasticity
5. Measured service
### On-demand self-service
Customer can automatically deploy resources (computing time, storage); no need for human interaction.

=> lowers load on admins; there is usually a user portal connected to an API
### Broad network access
Features are accessible by internet from different platforms (applications, browsers, phones, ...)
### Resource pooling (sharing) + Multitenance
Computing resources are grouped such that they serve multiple customers at the same time. This is achieved by using a multitenance model using virtualized machines that are dynamically allocated and reallocated between nodes depending on demand.

Users shouldn't be able to tell which node they are on or that some reallocations are happening or that there are other users using the machine.
#### Multitenance approaches
There are different ways of achieving multitenance in SaaS applications (IaaS applications):
- Application is the application itself
	- In IaaS: = Management Layer = deals with allocations, routers, network, automatization
- Database is the database that stores the user data
	- In IaaS: = Data layer = computing nodes, storage, network resources that are allocated to the users.
1. Separated deployment of application and each application has its own database (= own private cloud in a data center)
2. Shared application with different separated databases (= virtual private cloud)
3. Shared application with shared databases (= public cloud)

![[Pasted image 20240523141507.png]]

Goal is to have capabilities for approach #3.
### Rapid Elasticity
Resources are elastically controlled and allocated (manually or automatically); possibility of scaling up and down quickly depending on demand. User sees their resources as unlimited.

This is decision is made by some autoscaling algorithm that analyzes a time-series data of latency, load and communicates with the cloud API to scale.
### Measured Service

# IaaS
(Infrastracture as a Service)
It is a service for renting computing resources built upon virtualization.
It is one of the 3 layers of cloud computing and has to adhere to the definition of NIST.