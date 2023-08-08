---
title: "🐳 Essential docker interview topics : prepare for your upcoming interview📃"
seoTitle: "Essential docker interview topics : prepare for your interviews"
datePublished: Tue Aug 08 2023 17:38:56 GMT+0000 (Coordinated Universal Time)
cuid: cll2l5idb00020ami6njx25ub
slug: essential-docker-interview-topics-prepare-for-your-upcoming-interview
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691516107505/702a16fb-194e-4b60-b583-fa7bd1998229.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691516251196/11a7fe1a-a0ab-4403-8017-23fef1ee4b84.png
tags: docker, devops, 90daysofdevops, trainwithshubham, tws

---

## **📍** Introduction:

Introducing an AMAZING, all-inclusive list of must-know Docker interview questions, crafted just for YOU to CRUSH your DevOps interview! Don't miss out on these fantastic questions and get ready to ACE your interview like a PRO! 🚀🎉

## ✔ Let's start with the questions:

1. What is the Difference between an Image, Container and Engine?
    
    * **Docker image:**
        
        An image is a lightweight package that contains everything required to run the software, including the software code, dependencies, runtime, and environment variables.
        
        A Docker image is created using a Dockerfile, which contains specific instructions for constructing the image. The image is built in layers, starting with the base operating system, followed by the application code, and finally its dependencies.
        
    * **Docker container:**
        
        A Docker container can be described as a running instance of a Docker image. It executes the application in an isolated environment, meaning it is separate from both other containers and the host system.
        
        A container does not have its kernel but shares the host OS kernel, making them lightweight as they consume fewer resources.
        
2. What is the Difference between the Docker command COPY vs ADD?
    
    * `COPY:` The COPY command is an individual instruction in a docker image, we can use it to copy our source code from our host to the filesystem layer of the docker image. Its syntax is as follows `COPY <src> <dest>`
        
    * `ADD:` The add command also copies our source code into the filesystem layer of the docker image but we can also specify a URL and the ADD command will fetch the data from the remote and send it to the destination folder. It has also handy when we have a tarball to copy into a destination, docker will auto-extract it before sending it to the destination. The syntax of ADD command is as follows `ADD <src/URL> <dest>`
        
3. What is the Difference between the Docker command CMD vs RUN?
    
    * RUN: This command is used when creating a docker image, it helps us to install all the required dependencies for our project. The RUN command is executed in a shell i.e. `/bin/sh -c` and the output of this command is saved in the image's filesystem. For example, if we want to create a docker image for our nodejs project then we can run `npm install` in the RUN command
        
    * CMD: This command is executed when our container is created. The command specified in CMD is executed as the main process in our container. It is not executed when our image is being created.
        
4. How Will you reduce the size of the Docker image?
    
    Here are some steps that we can take to reduce the size of a docker image:
    
    * **use a smaller base image:** using a smaller base image instead of a fully-fledged image can help reduce the final image size. Images like Alpine Linux or busy box can be a good alternative. Or if you want extremely small images then use the `scratch` image and then copy all the required dependencies into it.
        
    * **utilize the .dockerignore file:** The .dockerignore file is similar to the .gitignore files. All the files or directories mentioned in the .dockerignore file will not be copied into the docker image filesystem layer.
        
    * **optimize steps in Dockerfile:** We can rearrange the steps in the Dockerfile to place them later in the sequence, allowing them to be cached and eliminating the need for rebuilding.
        
    * **multi-stage builds:** We can also utilize multi-stage builds, in this way we can build intermediate images that compile and build our application then copy only the necessary artifacts into our final image.
        
5. Why and when to use Docker?
    
    Docker is very helpful when we want to streamline our development and deployment processes. In the DevOps scenario Docker is most useful as it proves very helpful in
    
6. Explain the Docker components and how they interact with each other.
    
    The Docker engine comprises the Docker CLI and the Docker daemon. The Docker CLI is utilized for issuing commands to the Docker daemon, such as creating a Docker image or container.
    
    The Docker daemon is a service that constantly runs in the background, listening to commands given by the Docker CLI and executing them accordingly. Internally, the Docker daemon operates a service called containerd, which is also a daemon. Containerd is a container runtime that manages the container lifecycle, including tasks such as creating, deleting, and stopping containers.
    
7. Docker vs Hypervisor?
    
    Docker is software that enables us to create containers, which are lightweight packages designed to run our applications. A container contains the source code and its required dependencies to execute an application. Containers are lightweight because they do not have a kernel of their own they use the kernel of the host system.
    
    On the other hand, a hypervisor is software that enables us to create separate virtual machines, each with its operating system, while drawing resources from the host operating system to function. Since each virtual machine has its operating system, creating multiple virtual machines can significantly increase resource utilization.
    
8. What are the advantages and disadvantages of using docker?
    
    **Advantage:** Docker's primary advantage is its ability to create lightweight, portable containers that ensure consistent application performance across various environments. These containers provide rapid deployment, efficient resource utilization, and version control, and are essential for microservices architecture and DevOps practices, improving collaboration and scalability.
    
    **Disadvantage:** Docker can cause security issues because containers use the same host OS, so careful setup is needed to avoid risks. Handling lasting data, network problems, and resource conflicts can be difficult. While Docker makes using resources, growing, and setting up easier, managing images and organizing solutions need to be thought, so it's important to balance the good and bad aspects.
    
9. What is a Docker namespace?
    
    A namespace is a feature in the Linux system that separates different processes and environments. Docker and similar technologies use namespaces to make small, separate spaces for different tasks to run together on one computer.
    
10. What is a Docker registry?
    
    Just like the GitHub docker registry is a place where we can get officially published docker images like Ubuntu, docker, Nginx, MongoDB etc. as well as user-uploaded custom images.
    
11. What is an entry point?
    
    An ENTRYPOINT is a step in the docker file same as the CMD step both are used to specify the main executable within a container but the key difference is that the parameters specified in the CMD step can be overwritten when executing in the command line, but the parameters specified in ENTRYPOINT are not overwritten.
    
12. How to implement CI/CD in Docker?
    
    We can implement CI/CD in Docker by creating automated pipelines that build, execute, test, and deploy our code. We can pull the project files from GitHub and then use a Dockerfile to create images and run applications in containers.
    
13. Will data on the container be lost when the docker container exits?
    
    A Docker container is temporary, so all the data inside it gets erased when it is stopped or removed.
    
14. What is a Docker swarm?
    
    Docker Swarm is an orchestration tool that clusters all the hosts running the Docker daemon and configured to join the same cluster. Docker Swarm manages all the nodes running a Docker service.
    

What are the docker commands for the following:

* view running containers:
    
    `docker container ls`
    
* command to run the container under a specific name:
    
    `docker run -itd --name container_name docker_image`
    
* command to export a docker container:
    
    `docker commit container_id_or_name new_imge_name`
    
    `docker save -o output_file.tar docker_image`
    
    `docker load -i exported_file_name.tar`
    
* command to import an already existing docker image:
    
    `docker load -i exported_file_name.tar`
    
* commands to delete a container:
    
    `docker container rm container_name`
    
* command to remove all stopped containers, unused networks, build caches, and dangling images: `docker system prune -f`
    

## **📍** Conclusion:

These essential Docker interview questions will undoubtedly assist you in acing your interview. I have provided answers to these questions, and if you have any other valuable questions worth mentioning, please feel free to share them in the comments below. Your input is greatly appreciated!