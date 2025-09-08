## Kindly STAR 🌠 this repo if you find it helpful

# Containerization

## What is a container ?

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

A container is a bundle of Application, app libraries required to run your application with minimum system dependencies.

![Image1](https://user-images.githubusercontent.com/43399466/217262726-7cabcb5b-074d-45cc-950e-84f7119e7162.png)


## Containers vs Virtual Machine 

Containers and virtual machines are both technologies used to isolate applications and their dependencies, but they have some key differences:

    1. Resource Utilization: Containers share the host operating system kernel, making them lighter and faster than VMs. VMs have a full-fledged OS and hypervisor, making them more resource-intensive.

    2. Portability: Containers are designed to be portable and can run on any system with a compatible host operating system. VMs are less portable as they need a compatible hypervisor to run.

    3. Security: VMs provide a higher level of security as each VM has its own operating system and can be isolated from the host and other VMs. Containers provide less isolation, as they share the host operating system.

    4. Management: Managing containers is typically easier than managing VMs, as containers are designed to be lightweight and fast-moving.



## Why are containers light weight ?

Containers are lightweight because they use a technology called containerization, which allows them to share the host operating system's kernel and libraries, while still providing isolation for the application and its dependencies. This results in a smaller footprint compared to traditional virtual machines, as the containers do not need to include a full operating system. Additionally, Docker containers are designed to be minimal, only including what is necessary for the application to run, further reducing their size.

Let's try to understand this with an example:

Below is the screenshot of official ubuntu base image which you can use for your container. It's just ~ 22 MB, isn't it very small ? on a contrary if you look at official ubuntu VM image it will be close to ~ 2.3 GB. So the container base image is almost 100 times less than VM image.

![Image2](https://user-images.githubusercontent.com/43399466/217493284-85411ae0-b283-4475-9729-6b082e35fc7d.png)


To provide a better picture of files and folders that containers base images have and files and folders that containers use from host operating system (not 100 percent accurate -> varies from base image to base image). Refer below.


### Files and Folders in containers base images

```
    /bin: contains binary executable files, such as the ls, cp, and ps commands.

    /sbin: contains system binary executable files, such as the init and shutdown commands.

    /etc: contains configuration files for various system services.

    /lib: contains library files that are used by the binary executables.

    /usr: contains user-related files and utilities, such as applications, libraries, and documentation.

    /var: contains variable data, such as log files, spool files, and temporary files.

    /root: is the home directory of the root user.
```


### Files and Folders that containers use from host operating system

```
    The host's file system: Docker containers can access the host file system using bind mounts, which allow the container to read and write files in the host file system.

    Networking stack: The host's networking stack is used to provide network connectivity to the container. Docker containers can be connected to the host's network directly or through a virtual network.

    System calls: The host's kernel handles system calls from the container, which is how the container accesses the host's resources, such as CPU, memory, and I/O.

    Namespaces: Docker containers use Linux namespaces to create isolated environments for the container's processes. Namespaces provide isolation for resources such as the file system, process ID, and network.

    Control groups (cgroups): Docker containers use cgroups to limit and control the amount of resources, such as CPU, memory, and I/O, that a container can access.
    
```

It's important to note that while a container uses resources from the host operating system, it is still isolated from the host and other containers, so changes to the container do not affect the host or other containers.

**Note:** There are multiple ways to reduce your VM image size as well, but I am just talking about the default for easy comparision and understanding.

so, in a nutshell, container base images are typically smaller compared to VM images because they are designed to be minimalist and only contain the necessary components for running a specific application or service. VMs, on the other hand, emulate an entire operating system, including all its libraries, utilities, and system files, resulting in a much larger size. 

I hope it is now very clear why containers are light weight in nature.

<hr>

A home for my container learning, quick revisions, and production-style app containers.

- **`docker/`** → quick revision playground: tiny examples, beginner images, notes.
- **`apps/` (planned)** → real applications, each with its own Dockerfile and docs.
- **`compose/` (planned)** → Docker Compose stacks for local multi-service setups.
- **`k8s/` (planned)** → Kubernetes manifests / Helm charts.

> Keep experiments in `docker/`, and put real services in `apps/`. This separation keeps the repo tidy and avoids mixing throwaway examples with production-like code.

---

## Repository Structure

<pre>
Containerization/
├─ README.md
├─ docker/
│ └─ section-1/
│ └─ first-image/
│ ├─ Dockerfile
│ └─ app.py
├─ apps/ # planned
├─ compose/ # planned
└─ k8s/ # planned
</pre>

---

## Quick Start (current example)

Build and run the example located at `docker/section-1/first-image/`.

### 1) Build
```bash
docker build -t first-image:dev docker/section-1/first-image

# example I am using below command with docker user and repo details:-

docker build -t anshulawasthi03/first-image .

# or if you want to supply the path for your docker file

docker build -t anshulawasthi03/first-image docker/section-1/first-image
```
### 2) Run

Map the container port to your host (adjust ports to match the app inside the image—common choices are 5000 or 8000):

```bash
docker run --rm -it -p 8000:8000 first-image:dev
```
If your app.py serves on port 5000, use -p 5000:5000 instead.

### 3) Stop & Clean Up

Press Ctrl+C to stop an interactive container.

Optional cleanup:
```bash
docker ps -a
docker rm <container_id>        # remove stopped container
docker rmi first-image:dev      # remove image
```

### 4) Local Testing (without Docker)
```bash
cd docker/section-1/first-image
python app.py
```

If your app needs dependencies, add a requirements.txt here and install with:
```bash
pip install -r requirements.txt
```

### 5) Ignore Files

* Keep a root .gitignore for global dev artefacts (e.g., __pycache__/, *.log, venv/, node_modules/, .env).

* Keep a per-context .dockerignore next to each Dockerfile to keep images small:

<hr>
<hr>

## Helpful Docker Commands (Cheatsheet)

**Build with a tag**
```bash
docker build -t myimage:tag path/to/context
```

**Run interactively with port mapping**
```bash
docker run --rm -it -p HOSTPORT:CONTAINERPORT myimage:tag
```

**List images & containers**
```bash
docker images
docker ps -a
```

**Show logs**
```bash
docker logs -f <container_id_or_name>
```

**Restarted : A container can be restarted using the docker restart command which stops and then starts the container.**
```bash
docker restart my-container
```

** Paused : In the "paused" state, all processes inside the container are suspended. This is useful for temporarily halting a container without stopping it completely.**
Pause a container:
```bash
docker pause my-container
```
Resume a paused container:
```bash
docker unpause my-container
```

**Killed : The docker kill command forcefully stops a container by sending a SIGKILL signal to its processes.**
```bash
docker kill my-container
```

**Remove containers & images**
```bash
docker rm <container_id>
docker rmi <image_id_or_tag>
```
