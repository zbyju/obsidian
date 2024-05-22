**Principy virtualizace - emulace, paravirtualizace, plná virtualizace, hw. akcelerovaná virtualizace, hypervizor a jeho části, virtualizace paměti, virtualizace disků a V/V subsystému, virtualizace síťových zařízení, druhy migrace vituálních počítačů a disků.**

# Virtualizace
Virtualization is a technique of dividing resources of the real computer between several virtual ones. The management of virtual computers is done by hypervizor. There are 2 types of hypervizors:

![[Pasted image 20240522155753.png]]

1. Type 1 = Hypervizor runs directly above the hardware, it runs the virtual computers through the host's hardware.
2. Type 2 = Hypervizor runs above the operating system of the host computer, it runs the resources through the OS.
The hypervizor's task is to creates and manages virtual computers, hardware (CPU, GPU, RAM, I/O subsystem, network).

## x86/x64 Architecture
The x86/x64 architecture defines several rings - each ring/level has a set of instructions that can be ran in that layer. Layer 3 for example has lower privileges.

![[Pasted image 20240522160319.png]]

## Emulation
It's not truly a virtualization technique. Hypervizor = Emulator

It's implemented using software only and easily transferable. It is the slowest technique.

Examples:
- Qemu
- Wine
- CiscoPacketTracer
## Full Virtualization
Hypervizor emulates the whole hardware. This completely separates the hosted OS from the real hardware.

![[Pasted image 20240522161627.png]]

It uses a combination of *direct instruction execution* (přímé spouštění) and binary *translation of instructions*.

### Direct Execution
Does not effect the real computer and therefore they can be executed as they are. Also called *non-privileged* instructions.
### Binary Translation
These instructions would effect the real computer (e.g. working with I/O, interrupts) and are interrupted by the hypervizor and executed in a safe manner. These instructions are *privileged instructions*. It adds overhead.
## Paravirtualization
Hypervizor is called a Virtualization layer - it executes *Hypercalls*.

The hosted OS has a modified kernel and is aware that it is ran in a paravirtual environment. Hypercalls replace privileged instructions - hosted OS decides if the instruction is privileged and instead it calls the virtualization layer.

![[Pasted image 20240522163314.png]]
## Hardware-Assisted (Native) Virtualization
Only possible with hardware that supports virtualization.

Hosted OS is ran in ring 0; hardware detects privileged instructions and passes them to the hypervizor.
Hypervizor can run privileged instructions to manage virtual computers:
- VMXON - Activate virtualization mode
- VMXOFF - Deactivate virtualization mode

![[Pasted image 20240522163652.png]]
## Nested Virtualization
Virtualization running inside a running virtual computer. It might be efficient if both hypervizors communicate with each other without the real OS - this must be supported by both hypervizors and the OS.

![[Pasted image 20240522164152.png]]
## Container Virtualization
Instead of virtual computers we have containers. There are 2 types of containers:
1. Application container
2. Containers with operating systems

![[Pasted image 20240522164404.png]]![[Pasted image 20240522164832.png]]

### Application Container
Management of containers is done using a *Container Engine*. It only has libraries required for running the application + the application itself.

The container uses the kernel of the real OS. Containers are much smaller than virtual machines and much faster. They are used for deployment.

Example: Docker
### Containers with OS
They are closer to virtual machines but very limited as they must be compatible with the real OS.

The container has the base of an OS (libraries) but shares the kernel with the real OS. These containers have isolated virtual environments.

Example: LXC, OpenVZ
# Virtualization of Hardware Components
There are 2 strategies of virtualizing hardware (CPU, GPU, I/O, memory, network, ...):
- Software
	- Hypervizor emulates the behavior of different components.
	- Slow
	- Easy to transfer to other platforms
- Hardware Accelerated
	- Uses direct mapping to specific hardware of the real computer to its main memory.
	- Virtual computers have access to the hardware through the hypervizor, which has access to the main memory.
They both solve the same issues in different ways.
## Memory Virtualization
Each virtual computer has a Virtual Address Space; pages of VAS are stored in the Physical Memory. The main memory of the virtual computer is mapped to the main memory of the real computer (machine memory).

![[Pasted image 20240522173952.png]]

When looking up a content of a page from VAS we use VPN to PPN mapping. Virtual OS looks up the content in Physical Memory (it uses its own table to know where to look), the hypervizor then does the mapping from physical memory to machine memory.
### Shadow Paging
Hypervizor uses a shadow page for mapping physical addresses (PPN) to machine addresses (MPN). Hypervizor must intercept and modify the shadow page tables whenever guest OS modifies its own tables.
### Hardware-Accelerated Memory Access
The translation tables are maintained by the hardware; the CPU directly translates physical addresses to machine addresses.

This is faster, less overhead.

## I/O Virtualization
IOMMU (input output memory management unit) is the part of the hypervizor that does I/O virtualization.

IOMMU exists as software (emulation) or hardware accelerated.
### Emulation
All requests go through hypervizor which emulates the behavior.
### Hardware-Accelerated
IOMMU allows virtual computers access to the main memory which gives them direct access to devices.
Installed hardware needs to be mapped directly to the main memory.
## Network Virtualization
Hypervizor creates different virtual networks (it stores the information about them to the main memory). It emulates a network interface for each virtual computer. For the actual communication it uses the real hardware network card.

It uses NAT for virtual networks to separate virtual computers; it also runs its own DHCP server. It is possible to create a virtual bridge to connect the virtual network to the outside network or to other virtual networks.
# Migrations

# Virtual Networks
**Substrate** - the real 
Substrate

