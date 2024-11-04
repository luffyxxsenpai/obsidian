# docker
---
Date: 12,Oct,2024
subject: the theoretical world of docker
field: [[devops]] [[docker]] [[linux]] [[dockerfile]] [[docker-compose]] [[docker-volume]] [[docker-network]]
tags: #intro 

---

# 1. What is virtualization
it refers to creating virtual version of physical resources like servers, storage devices, or network devices. multiple vm's can run on a single physical machine, each with its own OS and applications.

### How Virtualization Works:

Virtualization involves using a **hypervisor** (like VMware, Hyper-V, or KVM) to create and manage virtual machines on a physical server. The hypervisor allocates resources such as CPU, memory, and storage to each VM and ensures isolation between them.

There are two types of hypervisors:

1. **Type 1 (Bare-metal hypervisors)**: These run directly on the hardware (e.g., VMware ESXi, Microsoft Hyper-V).
2. **Type 2 (Hosted hypervisors)**: These run on a host operating system (e.g., Oracle VirtualBox, VMware Workstation).



# 2. Containerization
**Containerization** is a lightweight form of virtualization that allows applications to run in isolated environments called **containers**. Unlike VMs, containers share the host system's kernel, making them more efficient and faster to start.

### How Containerization Works:

Containers package applications with all their dependencies, including libraries and binaries, but **without bundling a full OS**. They rely on the underlying host's kernel and only virtualize the user space. This makes containers much smaller and more resource-efficient than virtual machines.

Containers are managed using **container runtimes** like Docker, containerd, or runc. They rely on features in the Linux kernel, such as **namespaces** (for isolation) and **cgroups** (for resource limits), to function.

### Benefits of Containerization:

- **Lightweight**: Containers share the host OS kernel, so they don't need to bundle an entire operating system, reducing their size (megabytes instead of gigabytes for VMs).
- **Fast Start-up**: Containers can start in a matter of seconds (or even milliseconds), whereas VMs can take minutes.
- **Scalability**: Containers are ideal for microservices architectures, enabling quick scaling up and down of services.
- **Portability**: Containers encapsulate an application and its dependencies, making them portable across different environments (development, testing, and production).
- **Efficient Resource Use**: Containers use fewer resources because they don't require full guest OS installations. Multiple containers can share resources more efficiently on the same host.


# 3. Docker

### What is Docker?

**Docker** is a popular containerization platform that automates the deployment of applications inside containers. It simplifies the packaging, distribution, and running of applications by using standardized container images.

Docker provides developers with an easy-to-use interface for creating, deploying, and managing containers. It is widely adopted due to its simplicity, efficiency, and flexibility.

### Core Components of Docker:

#### **Docker Engine**:

- **Docker Engine** is the runtime environment for Docker containers. It includes both the Docker daemon (`dockerd`) and the client (`docker`) that interacts with the daemon.
- It allows you to build, run, and manage containers on any host that has Docker installed.

#### **Docker Daemon (`dockerd`)**:

- The **Docker daemon** is a background process that manages Docker containers on the host. It listens for API requests, manages container life cycles, builds images, and coordinates communication between containers and the Docker client.

#### **Docker CLI (`docker`)**:

- The **Docker CLI** (Command Line Interface) is the tool used to interact with the Docker daemon. Commands like `docker build`, `docker run`, `docker stop`, and `docker ps` allow you to manage images, containers, volumes, and networks.

#### **Docker Image**:

- A **Docker image** is a snapshot of an application and its dependencies. It is the blueprint used to create containers.
- Images are built using **Dockerfiles** and are stored in registries (e.g., Docker Hub, private registries).

#### **Docker Container**:

- A **container** is a runtime instance of a Docker image. Containers are isolated from each other and the host but can interact via networking if needed.

#### **Docker Registry**:

- A **Docker registry** is a storage and distribution system for Docker images. Docker Hub is the default public registry, but you can also run your own private registry.

### **Dockerfile**

A **Dockerfile** is a script containing a series of instructions to build a Docker image. It defines how an image should be built, specifying the base image, application code, dependencies, environment variables, and more.

####  **Docker Compose**

**Docker Compose** is a tool for defining and running multi-container Docker applications. Using a **`docker-compose.yml`** file, you can specify services, networks, and volumes for your entire application stack.



# 4. COMMANDS
`# Docker Essentials  ## Basic Commands and Operations  ### Viewing Docker Containers and Images  - **List Running Containers**:     ```bash   docker ps`

- **List All Containers (including stopped)**:
    `docker ps -
	
- **List Docker Images**:
    `docker images`
    
- **View Container Logs**:

    `docker logs <container_id>`
    
- **Inspect Container or Image**:

    `docker inspect <container_id_or_image_id>`
    

### Deleting Docker Containers and Images

- **Stop a Running Container** 
    `docker stop <container_id>`

- **Remove a Stopped Container**
    `docker rm <container_id>`
    
- **Remove an Image**:
    `docker rmi <image_id>`
    
- **Remove All Stopped Containers**:

    `docker container prune`
    
- **Remove All Unused Images**:
 
    `docker image prune`
    
- **Remove All Unused Containers, Networks, and Images**:
    `docker system prune`
    

### Basic Docker Operations

- **Run a New Container**:
    `docker run -d --name <container_name> <image_name>`
    
- **Execute Command in Running Container**:
    `docker exec -it <container_id> <command>`
    
- **Build an Image from Dockerfile**:
 
    `docker build -t <image_name>:<tag> <path_to_dockerfile>`
    
- **Tag an Image**:

    `docker tag <image_id> <repository>:<tag>`


---

