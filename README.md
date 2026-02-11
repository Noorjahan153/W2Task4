Agenda

* Explain the problem Docker solves
* Virtual Machines vs Docker
* Understanding Docker Architecture -  What gets installed when Docker is installed?
* Dockerfile Deep Dive - Explain each line 
* Key Docker Commands
* Docker Networking
* Volumes & Persistence
* Docker compose

**Step 1** — How apps worked earlier (NO Docker)

Imagine you create an application:

Example: Node app / Java app / Python app.

To run it, you need:

*Operating System
*Language runtime (Node / Python / Java)
*Libraries
*Configurations

So you install everything manually.

😵 Problem:

On your laptop → works
On server → doesn’t work

Because:

❌ Different OS
❌ Different versions
❌ Missing libraries

This is called: Environment mismatch
Also:
*Installing takes time
*Servers waste resources
*Scaling is hard

**Step 2** — Virtual Machines Came - VMs solved this by packing: App+Libraries+Full os 
Each VM has: Its own os, Huge size (GBs),Slow boot.

VM Structure-Hardware,Host os,Hyperviser,Guest OS,Application
VM Problems-Heavy,slow,Expensive,Each VM duplicates OS

**Step 3** - **Container(Docker)**
Docker said - Why carry Full OS Every time?
Instead: Use Host os Kernel and Only package: App+Libraries---> **These are called Containers**

What is virtualization---> Virtualization is the process of running multiple virtual systems or resources on top of a single physical machine.These resources could be a storage device,network or even an operating system!!
Eg: App         App          App
     |           |            |   
   Guest os    Guest os    Guest os
                |            
            Hypervisor
                 |
          Host Operating System
            









