# Virtual Machines 

A virtual machine manager, also called a hypervisor is a software that allows one to run a different OS with an OS. Examples include: VirtualBox, vmware. 

A virtual machine manager can creates many virtual machines and weach one can have a different OS in it. 

A virtual machine creates a virtual envionment that behaves like a complete computer system, complete with virtual hardware components. In a particular VM, the guest OS is stored on a virtual hard drive—a big, multi-gigabyte file stored on your real hard drive.Virtualization does add some overhead, so they aren't as fast as if you had installed the operating system on real hardware. 

You can also run multiple VMs at the same time, but you’ll find yourself somewhat limited by your system resources. Each VM eats up some CPU time, RAM, and other resources.

## Some uses of VM's

- They allow you to experiment with another OS without having to install it on your physical hardware. For example, they are a great way to mess around with Linux—or a new Linux distribution—and see if it feels right for you. When you’re done playing with an OS, you can just delete the VM.

- VMs also provide a way to run another OS’ software. For example, as a Linux or Mac user, you could install Windows in a VM to run Windows apps you might not otherwise have access to.

- Another advantage VMs provide is that they are “sandboxed” from the rest of your system. Software inside a VM can’t escape the VM to tamper with the rest of your system. This makes VMs a safe place to test apps—or websites—you don’t trust and see what they do.

## Examples of VM Apps

- VirtualBox: (Windows, Linux, Mac OS X): VirtualBox is very popular because it’s open-source and completely free.

- VMware Player: (Windows, Linux): You can use VMware Player on Windows or Linux as a free, basic virtual machine tool. More advanced features—many of which are found in VirtualBox for free—require upgrading to the paid VMware Workstation program. We recommend starting out with VirtualBox, but if it doesn’t work properly you may want to try VMware Player.

- VMware Fusion: (Mac OS X): Mac users must buy VMware Fusion to use a VMware product, since the free VMware Player isn’t available on a Mac. However, VMware Fusion is more polished.

- Parallels Desktop: (Mac OS X): Macs also have Parallels Desktop available. Both Parallels Desktop and VMware Fusion for Mac are more polished than the virtual machine programs on other platforms, since they’re marketed to average Mac users who might want to run Windows software.
 
From [here](https://www.howtogeek.com/196060/beginner-geek-how-to-create-and-use-virtual-machines/). It also contains some instructions/points on setting up a VM. 

[How to speed up your VM](https://www.howtogeek.com/124796/the-htg-guide-to-speeding-up-your-virtual-machines/).


## Some nice features of VMs

- VirtualBox can create snapshots that save a virtual machine’s state. You can revert to the saved state at any time by restoring a snapshot. 

- You can connect USB devices to your computer and expose them to the virtual machine as if they were connected directly. 

- VirtualBox allows you to set up “shared folders” that both the host operating system and guest operating system can access. 

- Shared Clipboard and Drag and Drop

- VirtualBox allows you to clone a virtual machine, creating a copy of it. 

## Docker Containers vs VMs 

Docker containers are not VMs. 
For VMs the hierarchy looks like : 
Infrastrcture > Host OS > Hypervisor > (Guest OS-1, Guest OS-2)>(Bins/Libs-1, Bins/Libs-2) > (App-1, App-2) 

For docker conatiner it looks like : 
Infrastructure > Host OS > Docker Daemon > (Bins/Lib-1, Bins/Lib2) > (App-1, App-2)

Docker containers take a lot less time to start up, they save resources, and isolate only apps and not entire systems unlike VMs. There is no virtualization in the case of docker.  

Often its necessary to run containers on top of VMs. 

VM’s are more secure, since containers make system calls directly to the Kernel. This opens up a whole verity of vulnerabilities.

For diff. between VMs, containers and virtual envs look [here](https://medium.com/@stephen.odaibo/docker-containers-python-virtual-environments-virtual-machines-d00aa9b8475).


## Hypervisors 

The hypervisor, also referred to as Virtual Machine Manager (VMM), is what enables virtualization (running several operating systems on one physical computer). It allows the host computer to share its resources between VMs.

2 types :
- Direct link to the infrastructure (HyperKit(Mac OSX), Hyper-V(win)). This makes them faster, simpler and hence more stable.
- Runs as an app on the host OS (vmware, virtualbox). This type of hypervisor is something like a “translator” that translates the guest operating system’s system calls into the host operating system’s system calls. The downside is that it creates a resource overhead, and multiple layers sitting on top of each other make things complicated and lowers the performance.


## Some questions ?

- Is it better to use VM's for certain tasks from a security POV(ethical hacking) ?




