---
title: "🔥 Getting started with docker volumes 💾and docker networks 🌐."
seoTitle: "🔥 Getting started with docker volumes 💾and docker networks 🌐."
datePublished: Thu Aug 03 2023 17:52:27 GMT+0000 (Coordinated Universal Time)
cuid: clkvgfmo100000ajzdkg0fjqh
slug: getting-started-with-docker-volumes-and-docker-networks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691084877376/efece744-be2a-4ad1-a1e0-41f09787b6d0.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691085092175/b58f5775-b7f9-4813-ab64-a3ee0e63417d.png
tags: docker, devops, docker-compose, 90daysofdevops, trainwithshubham

---

## **📍** Continuing from our [previous blog](https://yashraj-jaiswal.hashnode.dev/effortlessly-create-multiple-containers-using-docker-compose) post: 😊

WOW! Can you believe how AWESOME it's been diving into the world of docker-compose?! 🤩 In our last blog post, we covered some fundamental docker-compose configuration options. But in today's blog, we will be exploring more options to discover that'll help us tailor our docker containers to absolute PERFECTION! 🚀🎉

## ✔ Docker Volumes: 💾

Docker containers lack persistent file storage because they are isolated and possess only a virtual file system. Also, any data within a container is lost once it has been stopped. This is a significant issue if we want to maintain a database container.

![Volumes | Docker Documentation](https://docs.docker.com/storage/images/types-of-mounts-volume.png align="center")

Introducing Docker volumes, the preferred method for preserving data generated and utilized by Docker containers. Volumes are entirely managed by Docker, ensuring data persistence even when a container is removed.

Docker volumes let us connect a folder from our computer to a Docker container. When we change files in the container, the changes also happen on our computer. This way, even if the container stops, we still have the data. When the container starts again, the folder connects back, making the data available between restarts.

## ✔ Types of docker volumes:

### 🔸**Host volume:**

Host volumes preserve data even if the container is removed or stopped. This is particularly useful for scenarios where you want to update or replace a container without losing the data stored within it.

When creating a container, you can designate a host directory or file to be mounted within the container. This can be accomplished by using the -v or --volume flag in the docker run command.

Any changes made to the data in the volume from within the container are also reflected in the host system, and vice versa. This allows for seamless sharing of data between the host and the container, which is beneficial when you want to edit code on your local machine and have the changes directly propagated to the container.

```bash
docker run -d --name web-dev \
  -v /path/to/your/app:/app \
  -p 8000:80 \
  nginx:latest
```

With this setup, any changes you make to the code in /path/to/your/app on your host machine will be immediately reflected inside the container at /app. You can then access the application in your browser at http://localhost:8000.

Here's how you can specify host volumes in a docker-compose file:

```yaml
version: '3'

services:
  app:
    image: your-app-image
    volumes:
      - ./local-data:/app/data
```

### 🔸 Anonymous volume:

An anonymous volume in Docker refers to a type of volume that is created and managed by Docker itself without explicitly specifying a host directory or path. When you use an anonymous volume, Docker automatically manages the volume's creation, location, and lifecycle.

Anonymous volumes are tied to the lifecycle of the container that uses them. When the container is removed, the associated anonymous volume is also removed. They are particularly useful for temporary data, caches, or scenarios where data persistence is not a primary concern.

```bash
docker run -d --name log-generator \
  -v /app/logs \
  python:3.9 \
  sh -c "mkdir -p /app/logs && python /app/log_generator.py"
```

With this setup, the log files generated by the Python script will be stored in the anonymous volume specified by -v /app/logs. Even if you stop or remove the container using docker stop log-generator or docker rm log-generator, the log data will be preserved in the anonymous volume. However, keep in mind that you won't have direct control over the location of the data on the host system; Docker will manage it for you.

Here's how you can specify anonymous volumes in docker-compose file:

```yaml
version: '3'

services:
  app:
    image: your-app-image
    volumes:
      - /app/data
```

### 🔸 Named Volumes:

Named volumes in Docker are a way to manage and persist data between containers using user-defined names. Unlike anonymous volumes, which are managed by Docker and have auto-generated names, named volumes give you more control over where data is stored on the host system and allow you to share data between containers more predictably.

```bash
docker run -d \
  --name postgres-container \
  -e POSTGRES_PASSWORD=mysecretpassword \
  -v pgdata:/var/lib/postgresql/data \
  postgres:latest
```

In this example, the -v pgdata:/var/lib/postgresql/data flag specifies a named volume named pgdata for the PostgreSQL data directory. Docker will ensure that the data associated with this named volume is stored in a controlled location on the host system.

Here's how you can specify named volumes in docker-compose:

```yaml
version: '3'

services:
  app:
    image: your-app-image
    volumes:
      - data-volume:/app/data

volumes:
  data-volume:
```

## ✔ Docker Network: 🌐

In our previous blog, we containerized our Node.js application, which included a Node service, an Nginx service, and a MongoDB service. Have you ever wondered how the containers were able to communicate with each other, or how we were able to access the container services through the EC2 IP address?

Let's see the output on the screen when we use docker-compose to start containers. We can also use a handy command docker network ls to list all the available docker networks

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691031097876/4fd7919e-9179-4d62-a047-107733dbffaa.png align="center")

Upon executing the docker-compose command, we can observe that a network, named node\_docker\_default, was automatically created for us, with its driver type being a bridge.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691083866268/4ba069ee-5721-459b-883f-dca2e223bd23.png align="center")

Docker employs various driver types to achieve networking functionality. Let's examine some of the fundamental network types in Docker.

1. **Bridge network:**
    
    A bridge network in Docker is a type of virtual network that enables containers to communicate with one another and the host system. It is the default network type created when running Docker on a host machine. Bridge networks serve to isolate and segment containers from each other, offering a layer of network abstraction and security. Here's an example of specifying a bridge network in a docker-compose file.
    
    ```yaml
    version: '3'
    
    services:
      app:
        image: your-app-image
        networks:
          - my-bridge-network
    
    networks:
      my-bridge-network:
        driver: bridge
        external: false
    ```
    
2. **Overlay network:**
    
    An overlay network in Docker is a type of network that enables communication between containers running on different Docker hosts. Unlike bridge networks, which primarily facilitate communication between containers on the same host, overlay networks extend this capability to containers running on different hosts within a Docker swarm cluster.
    
    Docker swarm is a native clustering and orchestration solution provided by Docker for managing a group of Docker hosts as a single virtual host. Here's an example of specifying a overlay network in a docker-compose file.
    
    ```yaml
    version: '3.7'  # Note: Overlay networks require version 3.7 or higher
    
    services:
      app:
        image: your-app-image
        networks:
          - my-overlay-network
    
    networks:
      my-overlay-network:
        driver: overlay
    ```
    
3. **Host network:**
    
    The "host" network mode in Docker allows a container to directly share the networking namespace with the host machine. In this mode, the container does not get its isolated network stack; instead, it uses the same network stack as the host system.
    
    This means that the container and the host share the same network interfaces, IP addresses, ports, and routing table. Essentially, the container becomes a part of the host's networking environment. Here's an example of specifying a host network in a docker-compose file.
    
    ```yaml
    version: '3'
    
    services:
      app:
        image: your-app-image
        network_mode: host
    ```
    

## **📍** Conclusion:

In conclusion, Docker volumes and Docker networks are just mind-blowing!🤯 They offer such powerful tools for managing data persistence and container communication! By understanding and leveraging these fantastic options, developers can create super efficient and robust containerized applications, ensuring top-notch performance and adaptability in all sorts of scenarios! How awesome is that?!🎉🥳

There are various types of Docker networks besides bridge, overlay, and host. I will cover these in my upcoming blog posts.