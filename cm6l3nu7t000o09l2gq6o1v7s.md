---
title: "Understanding Docker and Container Lifecycle"
datePublished: Fri Jan 31 2025 18:30:44 GMT+0000 (Coordinated Universal Time)
cuid: cm6l3nu7t000o09l2gq6o1v7s
slug: understanding-docker-and-container-lifecycle
tags: docker, devops, containers, containerization

---

## Introduction

Today, I explored how **Docker Daemon (**`dockerd`**)**, **Docker Socket (**`docker.socket`**)**, and **Container Runtime (**`containerd`**)** interact. I also tested what happens when stopping Docker services and learned some interesting behaviors. Let's dive into it!

## Docker's Key Components

Before jumping into my experiments, here's a quick breakdown of key Docker components:

* **dockerd (Docker Daemon)**: This is the core service responsible for managing containers, images, networks, and volumes. It listens for requests from the Docker CLI and handles the overall lifecycle of containers.
    
* **docker.socket**: A systemd-managed socket that listens for Docker CLI API requests. If **dockerd** is not running, **docker.socket** can automatically start it. It's an essential part of Docker's client-server architecture.
    
* **containerd**: This is an industry-standard core container runtime that manages the complete container lifecycle, including image management, container execution, and supervision of containerized applications. It operates at a lower level compared to **dockerd** and is used by Docker to handle containers at runtime.
    
* **containerd-shim**: This lightweight process is responsible for managing container lifecycles. It ensures containers remain running even if **containerd** itself stops, facilitating detached execution of containers. It’s part of the reason Docker containers can persist even when **containerd** restarts.
    
* **runc**: The low-level runtime that interacts directly with the Linux kernel. **runc** implements the Open Container Initiative (OCI) runtime specifications, setting up namespaces, cgroups, and other container isolation mechanisms. It is the key component that actually creates and runs the containers.
    
* **libcontainer**: This is the earlier Go library used by Docker to create containers. It was refactored into **runc** when Docker started conforming to OCI standards. It provides the core functions of container creation and isolation.
    
* **OCI (Open Container Initiative)**: This set of open standards ensures interoperability between different container runtimes and images, allowing you to use containers across various platforms and runtimes.
    

## What Happens When You Stop `dockerd`?

I ran the following command to **stop Docker Daemon (**`dockerd`**)**:

```bash
sudo systemctl stop docker
```

Then, I checked its status:

```bash
sudo systemctl status docker
```

### Observations:

* `docker.service` (dockerd) was **stopped**.
    
* However, `docker.socket` **was still active!**
    
* Running `docker ps` worked, The reason? `docker.socket` **was still active**, so when I ran `docker ps`, it automatically restarted `dockerd` in the background.
    

## Fully Stopping Docker (Including `docker.socket`)

To **completely stop Docker**, I ran:

```bash
sudo systemctl stop docker.socket
```

Now, running `docker run busybox` gave an error:

```bash
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

This confirmed that without `docker.socket`, `dockerd` could not restart automatically.

### The Role of containerd, containerd-shim, runc, and libcontainer

While experimenting with Docker, I also explored how **containerd**, **containerd-shim**, **runc**, and **libcontainer** play key roles in container lifecycle management.

1. **containerd**:
    
    * After **dockerd** starts a container, **containerd** takes over. It handles lower-level operations like running and managing the container's lifecycle, including pulling images, creating containers, and managing namespaces and cgroups.
        
2. **containerd-shim**:
    
    * When **containerd** manages the containers, it uses the **containerd-shim** to ensure that containers continue running independently of **containerd**'s process. This allows containers to persist even if **containerd** itself stops.
        
3. **runc**:
    
    * **runc** is invoked by **containerd** to create and run containers. It interacts with the Linux kernel to set up the necessary namespaces and cgroups to isolate the container. When **containerd** needs to run a container, it uses **runc** to actually launch it in the specified environment.
        
4. **libcontainer**:
    
    * Although **libcontainer** is no longer used directly in most modern setups, its concepts are the foundation of **runc** and **containerd**. It was the original implementation used by Docker to handle container creation and isolation. Today, it is replaced by **runc**, which conforms to the OCI standards.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738340152505/090d83e2-68e4-448a-85e2-a29d36508266.png align="center")

Even if `containerd` is stopped, any existing containers continue running because they are managed by `containerd-shim`, which keeps the container alive. However, you won't be able to start new containers through Docker (`dockerd`), as it relies on `containerd` to create and manage containers. Instead, you can interact directly with `containerd` using the `ctr` CLI, which allows you to manage containers even when `dockerd` is not functional. Alternatives for `dockerd` are podman, rkt, etc

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738383763209/35cd8b0d-c495-42b5-b966-e45e254b770a.png align="center")

### Conclusion

Through this exploration, I learned that Docker relies on a series of components working together to manage container lifecycles and ensure smooth operation. Stopping **dockerd** doesn't completely stop Docker—**docker.socket** ensures that it can be restarted automatically when needed. I also explored how **containerd**, **containerd-shim**, **runc**, and **libcontainer** fit into the container ecosystem, each handling different aspects of container management, from execution to isolation.

By understanding the interactions between these components, you can gain deeper insight into how containers work and how Docker orchestrates everything behind the scenes.