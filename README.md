**Agenda**

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

* Operating System
* Language runtime (Node / Python / Java)
* Libraries
* Configurations

So you install everything manually.

😵 Problem:

On your laptop → works, On server → doesn’t work

Because:

❌ Different OS
❌ Different versions
❌ Missing libraries

This is called: Environment mismatch
Also:
* Installing takes time
* Servers waste resources
* Scaling is hard

**Step 2** — Virtual Machines Came - VMs solved this by packing: App+Libraries+Full os 
Each VM has: Its own os, Huge size (GBs),Slow boot.

VM Structure-Hardware,Host os,Hyperviser,Guest OS,Application
VM Problems-Heavy,slow,Expensive,Each VM duplicates OS

**Step 3** - **Container(Docker)**
Docker said - Why carry Full OS Every time?
Instead: Use Host os Kernel and Only package: App+Libraries---> **These are called Containers**

What is virtualization---> Virtualization is the process of running multiple virtual systems or resources on top of a single physical machine.These resources could be a storage device,network or even an operating system!!

Eg: ### Virtual Machine Architecture

```
+---------+   +---------+   +---------+
|  App    |   |  App    |   |  App    |
+---------+   +---------+   +---------+
| GuestOS |   | GuestOS |   | GuestOS |
+-------------------------------------+
              Hypervisor
+-------------------------------------+
          Host Operating System
+-------------------------------------+
              Hardware
```

What is Containerization?---> Application Containerization is an OS-level Virtualization method used to deploy and run distributed applications without launching an entire virtual machine(VM)for each app.

### Docker / Container Architecture

```
+--------+    +--------+    +--------+
| App 1  |    | App 2  |    | App 3  |
+--------+    +--------+    +--------+
|Bins/Libs|   |Bins/Libs|   |Bins/Libs|
+------------------------------------+
           Container Engine (Docker)
+------------------------------------+
                    OS
+------------------------------------+
                 Hardware
```

 ❌ Problems Before Containers

* Code worked on developer system but failed in production

* VMs consumed too many resources

* VMs were large and hard to move

* Environment mismatch

✅ How Containers Solved These Problems

* Lightweight

* Portable

* Same environment everywhere

* Developer friendly

 📦 Advantages of Containers

* Not resource hungry

* Small in size

* Highly portable

* Easy configuration using code

**🔧 Containerization Tools** --> MESOS,rkt,docker- Docker is clearly the most famous among them all!

**What is Docker?** --> Docker is a computer program that performs operating system level virtualization,also known as **Containerization**. It was first released in 2013 and developed by docker,Inc.Docker is used to run software packages called **Containers**.

          Docker container life cycle

                  Docker Hub
                      ▲
                      | Push
                      |
                  Pull|
                      ▼
                Docker Engine
                      |
                 Docker Images
                      |
                Containers stages
                      |
    -----------------------------------------
    |                |                     |
  Run              Stop                  Delete
    |                                     |
    ---------------------------------------
                      


🌐 Components of Docker Ecosystem

* Docker Hub -->Docker Hub is a central public docker registry. It can store custom docker images.The service is free, but your images would be public. It requires username/password.

* Docker Engine--> Docker Engine is the heart of the docker ecosystem, It is responsible for managing your container runtimes,It works on top of operating system level,It utilizes the kernel of the underlying OS.

* Docker Images-->Docker Image is like the template of a container, It is created in layers,Any new changes in the image results in creating a new layer,One can launch multiple containers from a single docker image.

* Docker Containers-->A Docker Container is a lightweight software environment,It works on top of the underlying OS kernel,It is small in size and therefore is highly portable,It is created using the docker image.

* Docker Volumes-->Docker Containers cannot persist data, To persist data in containers, we can use Docker Volume,A Docker Volume can connect to multiple containers simultaneously,If not created explicitly, a volume is automatically created when we create a container.

* Dockerfile--> Dockerfile is a YAML file, which is used to create custom containers,It can include commands that have to be run on the command line,This Dockerfile can be used to build custom container images.

  **Common Docker commands**

* **docker --version** --> This command helps you know the installed version of the docker software on the system.
* **docker pull <image-name>**-->This command helps you know the central docker repository.Eg: docker pull ubuntu
* **docker images**-->This command helps you in listing all the docker images downloaded on your system.
* **docker run <image-name>**-->This command helps in running containers from their image name. Eg:docker run -it -d ubuntu
* **docker ps**-->This command helps in listing all the containers which are running in the system.
* **docker ps -a**  -->if there are any stopped containers,they can be seen by adding the -a flag in this command.
* **docker exec <container-id>**-->For logging into/accessing the container,one can use the exec command.Eg: docker exec -it 233e926091f3 bash
* **docker stop <container-id>** -->For stopping a running conatainer,we use the stop command.Eg:docker stop 233e926091f3
* **docker kill <container-id>** -->This command kills the conatiner by stopping its execution immediately. The difference between **docker kill** and **docker stop** : 'Docker stop' gives the container time to shutdown gracefully;whereas,in situations when it is taking too much time for getting the conatiner to stop,one can opt to kill it. Rg:docker kill 233e926091f3
* **docker rm <container-id>** --> To Remove a stopped container from the system,we use the **rm** command eg:docker rm 233e926091f3
* **docker rmi <image-id>** --> To remove an image from the system, we use the rmi command.













            









