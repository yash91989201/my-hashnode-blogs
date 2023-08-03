---
title: "🐳Getting started with Docker for DevOps. 🔥🔥"
seoTitle: "Docker DevOps: Beginner's Guide"
seoDescription: "Master Docker with a beginner-friendly guide; learn container creation, deployment, management, and ensure seamless application performance in DevOps"
datePublished: Sun Jul 30 2023 17:40:37 GMT+0000 (Coordinated Universal Time)
cuid: clkpq907g000b09l8bq69bbhd
slug: getting-started-with-docker-for-devops
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690738736578/4bfba3e2-1b08-462e-84ea-80334b983e9e.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690738795966/80bfa039-4f80-44b0-b139-33f81b431fa0.png
tags: linux, docker, devops, 90daysofdevops, trainwithshubham

---

## **📍** Let's start with Docker: 🥳

Hey there readers 👋!!! Up until now, I've been sharing awesome content on Linux, bash scripting, git, GitHub, and Python, but guess what? The time has finally come to dive into Docker, the most crucial and widely-used tool in the DevOps world! So, without any further ado, let's jump right in and start exploring the fantastic world of Docker! 🚀🎉

## ✔ Let's understand what Docker is. 🤔

Consider the following scenario, imagine you've developed an impressive application that runs smoothly on your machine. You share this application with your friends so they can try it out. However, when they attempt to run the application, they encounter errors such as missing packages or absent modules.

![A General Docker Tutorial - openshift101](https://3046199028-files.gitbook.io/~/files/v0/b/gitbook-legacy-files/o/assets%2F-Lo1CthFUNGt5R3JtwjG%2F-M4KE4U8jUEv54EQtSJQ%2F-M0KOKi97XMUBcY4FQsW%2Fassets_-LtBxDkdPh1ZKmLAzW5v_-Ltht0_vGCm5brrUQOK2_-Lthvuq8uvz3mrYS5g_n_image.png?generation=1586272963682285&alt=media align="left")

Here's where Docker comes into play. In a nutshell, Docker packages software into standardized units called containers, which include everything the software needs to run, such as libraries, system tools, code, and runtime. With Docker, you can quickly deploy and scale applications in any environment, confident that your code will run smoothly.

## ✔ Okay cool, but how does Docker work? ⚙️

### 🔸 Docker architecture: 🏗

Under the hood, Docker utilizes a client-server architecture to perform its various functions. In this setup, the client serves as an interface, issuing commands to the Docker daemon (if you're unfamiliar with daemons, you can learn more about them [here](https://yashraj-jaiswal.hashnode.dev/a-guide-to-managing-services-and-packages-in-linux#heading-understanding-processes-daemons-and-services) ). The Docker daemon runs continuously in the background, receiving commands from the Docker client and executing the necessary tasks, such as building an image or running a container.

![Docker Architecture | How Docker Works? | Edureka](https://www.edureka.co/blog/wp-content/uploads/2019/09/Picture1-15.png align="center")

The Docker client and daemon can work together on one computer, or the client can connect to a daemon on another computer. They interact with each other using a simple web-based language, either through UNIX sockets or over a network. Docker Compose is another client that helps manage multiple containers in an application.

![Docker Objects. Dockerfile | by Bikram | Medium](https://miro.medium.com/v2/resize:fit:1079/1*3ds-PdxGGMN-ZzJH95_lsA.png align="left")

### 🔸 Dockerfile: 📁

Dockerfile is a simple text file that consists of instructions to build Docker images. In the Dockerfile we can specify the base image on which the container will run, where the application code will be kept within the container, and commands to execute when starting a container. We will explore this further in upcoming blog posts.

### 🔸 Docker Image: 📜

Images are **read-only templates** containing instructions for creating a container. A Docker image creates containers to run on the Docker platform. Think of an image as a blueprint or snapshot of what will be in a container when it runs.

An image consists of multiple stacked layers, starting with the base OS. Following that, you have your application code, and the other layers include the runtime, dependencies, and any additional file systems necessary for your application to run within a container. For example, to build a web server image, start with an image that includes Ubuntu Linux (a base OS). Then, add packages like Apache and PHP on top.

### 🔸 Docker Container: 📦

A container is like a package that wraps up your software code along with all its dependencies so that your app can run smoothly and reliably, no matter where you put it to work. We can use the docker image to create any number of docker containers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690731155965/d4b3cae1-daf7-4ad0-ba70-ddd2619bcebc.png align="center")

When creating a container, we can designate network ports to which the container will respond (these can be the ports your application runs on), ensuring the container's security as there are no random open ports to exploit.

### 🔸 Docker Hub: 🏙️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690731667074/fadbc46c-c5f8-42dd-91cf-ad8ef87cc8ae.png align="center")

Similar to GitHub, Docker Hub is a platform where you can find both official and user-created Docker images. Numerous official Docker images are available, such as Linux, MongoDB, Express, and many more, which allow you to build your applications on top of them.

You can also create an account on Docker Hub and publish your Docker images there for others to use.

## ✔ Basic Docker commands:

Alright, now that we've covered the basics, let's dive into some hands-on practice with Docker commands and have fun running a few containers together!

1. `docker run`: with this command, we can create new containers by specifying the Docker image. In the below example, we run a hello-world container.
    
    ```bash
    ubuntu@learn-linux:~$ docker run hello-world
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    719385e32844: Pull complete
    Digest: sha256:926fac19d22aa2d60f1a276b66a20eb765fbeea2db5dbdaafeb456ad8ce81598
    Status: Downloaded newer image for hello-world:latest
    
    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    ```
    
2. `docker inspect`: This command shows information about a specific container or an image. `run docker run -d -p 80:80 --name web-server nginx` to create a nginx container. Here, you can see that the `docker inspect` command provides a vast array of information for the container "web-server."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690734725240/9fb777e6-1fb8-4aad-9633-f89a813ccf0f.png align="center")
    
3. `docker port`: This command displays the port mappings of a container. We can execute this command on our Nginx container named "web-server." Here, we can observe that there is a port mapping for 80, which indicates that the "web-server" container can only be accessed on port 80 from the outside world.
    
    ```bash
    ubuntu@learn-linux:~$ docker port web-server
    80/tcp -> 0.0.0.0:80
    80/tcp -> :::80
    ```
    
4. `docker stats`: This command shows the resource usage and statistics of a container. `run docker stats web-server` to check the stats of our nginx container.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690734945487/f9cc889b-0ccb-4ae3-9e3a-e0024ac69df0.png align="center")
    
5. `docker top:` This command shows the running processes inside a container, much like executing the `top` command in Linux.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690735099943/28d71fc2-ff8a-49ea-90cb-4f0b394fa77a.png align="center")
    
6. `docker exec`: This command allows us to enter inside a container and execute commands. To exit the container just execute `exit` command.
    
    ```bash
    ubuntu@learn-linux:~$ docker exec -it web-server bash
    root@5bd7a99b9423:/#
    root@5bd7a99b9423:/# echo hello world
    hello world
    root@5bd7a99b9423:/# exit
    exit
    ubuntu@learn-linux:~$
    ```
    
7. `docker container ls`: This command shows the currently running containers. To see all the containers use `docker container ls -a`.
    
    ```bash
    ubuntu@learn-linux:~$ docker container ls
    CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                               NAMES
    5bd7a99b9423   nginx     "/docker-entrypoint.…"   12 minutes ago   Up 12 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   web-server
    ```
    
8. `docker image ls`: This command shows all the docker images available locally.
    
    ```bash
    ubuntu@learn-linux:~$ docker image ls
    REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
    nginx         latest    89da1fb6dcb9   2 days ago     187MB
    ubuntu        latest    5a81c4b8502e   4 weeks ago    77.8MB
    hello-world   latest    9c7a54a9a43c   2 months ago   13.3kB
    ```
    

## ✔ Let's talk about the benefits of Docker in DevOps.

Docker helps in DevOps as it is utilized by developers, testers, and system administrators alike. Developers create Docker images on their computers and execute them. System administrators employ the same images in staging and production environments.

Docker and DevOps enable collaboration among various teams throughout a software's lifecycle. They offer numerous benefits for development, business, and culture, but also present certain drawbacks. Fortunately, using both in tandem can help surmount these challenges.

## **📍** Definitely not the end...🤓

This is merely the tip of the iceberg; there is so much more to explore in Docker!! We've got docker volumes, docker networking, docker-compose, and so much more! I can't wait to dive into these topics in future blog posts. In the meantime, keep learning and practicing - it's going to be a thrilling journey! 🚀🎉. Here's a [blog](https://spacelift.io/blog/docker-tutorial) worth reading that provides further insights into Docker.

I hope you learned something new today. If you enjoyed reading this blog, do share what you found fascinating about Docker and any suggestions for improving my blog would be greatly appreciated.