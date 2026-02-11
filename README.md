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

**Virtual Machines vs Docker**

Virtual Machines:
- Heavy
- Full Guest OS
- Slow boot
- Large size (GBs)

Docker Containers:
- Lightweight
- No Guest OS
- Fast startup
- Small size (MBs)

— Virtual Machines Came - VMs solved this by packing: App+Libraries+Full os 
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
  Run                 Stop                    Delete
  
                      

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

**Dockerfile-Deepdive**

A Dockerfile is a text file that contains a set of instructions used to automatically build a Docker image.

It defines:

* Which base image to use
* What software to install
* What files to copy
* Which commands to run
* How the container should start

--> Using a Dockerfile, we can create custom Docker images in a repeatable and automated way.

--> Docker reads the Dockerfile line by line and executes each instruction to build the image.

In short:

👉 Dockerfile = Blueprint of a Docker Image

* FROM ubuntu - FROM defines the base image for the Docker image.
* RUN apt-get update - RUN executes commands while building the Docker image.
* RUN apt-get install -y apache2 

   apt-get update updates package lists.

   apt-get install -y apache2 installs the Apache web server.

Each RUN creates a new layer in the Docker image.
* ADD . /var/www/html - ADD copies files from the local system into the Docker image.

   . → Current project folder (local system)

  /var/www/html → Apache web root inside container

This copies all website files into Apache so it can serve them.
👉 Without ADD, Apache runs but shows no webpage.
* CMD apachectl -D FOREGROUND - CMD specifies the default command that runs when the container starts.

This starts the Apache server and keeps it running in the foreground.

👉 If Apache runs in background, container stops.
👉 Foreground keeps container alive.
* Entrypoint - The Entrypoint keyword is used strictly to run commands the moment the container initializes. The difference between CMD and ENTRYPOINT , ENTRYPOINT will run irrespective of the fact whether the argument is specified or not.

  ENTRYPOINT apachectl-D FOREGROUND
* ENV - The ENV keyword is used to define environment variables in the conatainer runtime. Like ENV name DEVOPS PearThoughts

  **DOCKER COMPOSE**

"Compose is a tool for defining and running multi-container Docker applications.With compose, you use a YAML file to configure your application's services. Then, with a single command ,you create and start all the services from your configuration.Run docker-compose up and compose starts and runs your entire app".

**What are yaml files?**

YAML is a superset of a JSON file.There are only two types of structures in YAML which you need to know to get started: **MAPS and Lists**

MAPS- when we map a key to a value in YAML files, they are termed as Maps.
* <Key><Value> eg : Name:Pearlthoughts
                    Course:Devops

Lists - YAML lists are a sequence of objects.
  Args
  * arg 1
  * arg 2
  * arg 3
->Eg:args
    - sleep
    - "1000"
    - message
    - "Bring back firefly!"

**Sample Writing a Docker Compose File**


  













            









