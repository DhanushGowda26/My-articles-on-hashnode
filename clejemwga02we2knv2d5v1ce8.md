---
title: "An extended version to know more of Docker"
seoTitle: "Gearing up Docker to an intermediate level"
seoDescription: "Docker knowledge blog  up to an intermediate level where yoy will learn lot of docker concepts like its architecure, networking, volume and lot more."
datePublished: Sat Feb 25 2023 03:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clejemwga02we2knv2d5v1ce8
slug: an-extended-version-to-know-more-of-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1677246664140/5b8e94fe-f76f-430e-97dd-32efe4629155.png
tags: docker, development, developer, devops

---

### **Docker Architecture**

It is composed of several components that work together to enable containerization. Here's a breakdown of each component and how they fit together:

Docker Client: The Docker client is the command-line tool that you use to interact with Docker. It sends commands to the Docker daemon (server) and receives output in response.

Docker Daemon: The Docker daemon is the background process that runs on the host machine and manages all aspects of the Docker environment. It listens for requests from the Docker client and manages the creation, running, and destruction of Docker containers.

Docker Registry: The Docker registry is a centralized location for storing and distributing Docker images. It contains a collection of repositories, each of which contains one or more tagged images. The most commonly used Docker registry is Docker Hub, but you can also use private registries for added security.

In summary, the Docker architecture consists of a client-server model, where the Docker client sends requests to the Docker daemon, which manages containers, images, volumes, and networks. Docker images are stored in a registry, and Docker containers are lightweight, standalone packages that can be easily created, started, stopped, and deleted.

### Why Networking?

While the purpose of containers is to provide isolated environments to run applications, they are often not intended to run in isolation forever. There are several reasons why you might need to connect containers or to the outside world.

Microservices architecture: Many modern applications are built using a microservices architecture, where different components of the application are split into separate services running in different containers. These services often need to communicate with each other over the network to function properly.

Scaling: One of the advantages of using containers is that you can easily scale your application up or down by running more or fewer containers. To ensure that your application is scalable, you need to be able to communicate between the different instances of your containers.

Data sharing: Sometimes, multiple containers need to share data or resources. For example, a web server container might need to access a database container to retrieve data.

Integration with external services: Containers often need to integrate with external services, such as a cloud storage provider or an API service.

So, while the primary purpose of containers is isolation, they often need to communicate with other containers or external services to function properly in a larger application or system.

### Docker Network

A docker network is a virtual network that allows containers to communicate with each other, as well as with the host machine and other networks. By default, Docker creates a bridge network when it is installed, but you can create additional networks for more fine-grained control over connectivity.

Example:

```bash
docker network create my-network

docker run -d --name container1 --network my-network image1
docker run -d --name container2 --network my-network image2
docker run -d --name container3 --network my-network image3
```

In this example, we first create a network called "my-network" using the docker network create command. Then, we start three containers (container1, container2, and container3) and specify the --network my-network flag to connect them to the "my-network" network.

Note that you can connect existing containers to a network using the docker network connect command. For example, if you have an existing container named "mycontainer" and you want to connect it to the "my-network" network, you can use the following command:

```bash
docker network connect my-network mycontainer
```

### Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It allows you to describe the services that make up your application in a YAML file and then start and stop all the containers that belong to your application with a single command.

Here is an example of a docker-compose.yml file that defines two services: a web service and a database service.

```yaml
version: '3'

services:
  web:
    build: .
    ports:
      - "5000:5000"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

In this file, the web service is defined to build an image from the Dockerfile in the current directory, and map port 5000 on the host to port 5000 in the container. The db service is defined to use the official postgres image, set an environment variable to specify the password for the database, and use the default port (5432).

To start these services, you can run the following command in the same directory as the `docker-compose.yml` file:

```bash
docker-compose up
```

This will start both services and output their logs to the console. If you want to run the services in the background, you can add the -d option:

```bash
docker-compose up -d
```

To stop the services, you can run:

```bash
docker-compose down
```

Overall, Docker Compose is a powerful tool for managing complex, multi-container Docker applications, and can save you time and effort when working with these types of applications.

### Docker Volume

In Docker, a volume is a way to store and manage data that is persistent across container instances. A Docker volume is a directory on the host filesystem that is mounted into a container at a specific path. This allows containers to access and modify the data stored in the volume even if the container is destroyed or recreated.

A Docker volume is created using the 'docker volume create command'. This creates a new directory on the host filesystem that is used to store data.

Volumes can also be created automatically when a container is started using the 'docker run command' with the '--mount' or '-v' flag. This binds a host directory to a directory in the container, creating a new volume if one with the specified name does not exist.

Volumes can be shared between multiple containers, allowing them to access the same data. This is useful for cases where multiple containers need to access a shared database or other data. Volumes can be backed up and restored, making it easy to migrate data between hosts or perform backups. When a volume is no longer needed, it can be removed using the docker volume rm command.

Suppose you have an application that writes data to a file. You want to run this application in a Docker container, but you also want the data to be persistent so that it can be accessed by other containers even if the original container is deleted. To do this, you can create a Docker volume and mount it into the container at a specific path.

First, create a Docker volume using the `docker volume create` command:

```bash
docker volume create mydata
```

This creates a new volume called "mydata" that can be used to store data.

`mydata` is a Docker volume, which means it's not located in any specific directory on your local machine. When you create a Docker volume using the `docker volume create` command, Docker creates a directory on the host machine where the volume is stored, but the exact location of this directory depends on your Docker installation and configuration.You can use the `docker volume inspect` command to see the details of a specific Docker volume, including the location of the directory where the volume is stored.

Next, start a new container using the `--mount` or `-v` flag to mount the "mydata" volume into the container at the path "/data":

```bash
docker run -d --name mycontainer --mount source=mydata,target=/data myimage
```

This command starts a new container based on the "myimage" image and mounts the "mydata" volume at the path "/data" inside the container. Now, any data written to the "/data" directory inside the container will be stored in the "mydata" volume on the host filesystem.

If you want to start a new container that can access the same data, you can simply mount the "mydata" volume into the new container using the same command:

```bash
docker run -d --name myothercontainer --mount source=mydata,target=/data myimage
```

This command starts a new container called "myothercontainer" and mounts the "mydata" volume at the path "/data" inside the container. Now, both containers can access and modify the same data stored in the "mydata" volume.

### Docker Security

Docker provides several security features that can be used to help protect your containers and their contents. These include security profiles for containers, which allow you to restrict the resources that a container can access the ability to run containers as non-root users, which helps to reduce the impact of security vulnerabilities and Docker Content Trust, which allows you to sign and verify the integrity of Docker images.

### Docker Swarm

Docker Swarm is a container orchestration tool that allows you to manage a group of Docker containers as a single virtual system. It is an open-source tool that is part of the Docker ecosystem, and it is designed to make it easier to deploy and manage containerized applications at scale. In the docker swarm, you can create a cluster of Docker hosts and deploy containers across the cluster. The containers are automatically distributed across the hosts, and Docker Swarm provides built-in load balancing and scaling capabilities.

Docker Swarm uses a manager-worker architecture, where one or more manager nodes are responsible for managing the cluster and scheduling tasks to worker nodes. Worker nodes are responsible for running the Docker containers. Docker Swarm also provides features such as service discovery, health checks, rolling updates, and secrets management to help you manage your applications more effectively

\*will try to explain docker security and swarm in detail in the next version of the docker blog.

### Docker Hub

Docker Hub is a cloud-based registry service that allows you to store and share Docker images with others. It provides a central repository for Docker images, making it easy to distribute and collaborate on containerized applications. You can use Docker Hub to:

* Store and manage your own Docker images.
    
* Find and download existing Docker images created by other users.
    
* Collaborate with others by sharing Docker images and collaborating on projects.
    

[Docker Hub official website](https://hub.docker.com/)

That's the end, I hope you learnt something new and Thanks for spending your time in learning.