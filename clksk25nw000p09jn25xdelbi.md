---
title: "😎 Effortlessly create multiple containers using docker compose. 🐳📜"
seoTitle: "😎 Effortlessly Create Multiple Containers Using docker compose. 🐳📜"
datePublished: Tue Aug 01 2023 17:10:38 GMT+0000 (Coordinated Universal Time)
cuid: clksk25nw000p09jn25xdelbi
slug: effortlessly-create-multiple-containers-using-docker-compose
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690909653333/60fc0f1f-92ea-4194-b188-98b322b3405d.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690909829191/169720e9-6a5e-4843-85e5-d98fcc9db645.png
tags: docker, devops, docker-compose, 90daysofdevops, trainwithshubham

---

In my [previous blog](https://yashraj-jaiswal.hashnode.dev/getting-started-with-docker-for-devops), I explained the process of creating a Docker container using a Dockerfile. We generated an image from it and ran that image to get a container.

The containerization process is truly impressive, but what about situations where we have a fairly large application with multiple requirements, such as a database, a Redis cache, a frontend, and a backend? Some of these components may be dependent on one another, so how can use the `docker run` command to manage all these containers effectively?🤔 The answer is ..... we don't😜, we can use a tool called docker-compose.

## **📍** What's a Docker compose? 🧐

![A few tricks on how to set up related Docker images with docker-compose -  Event-Driven.io](https://event-driven.io/static/67fd4c42f3de35627317b5d2fe97ce92/00d43/2022-05-11-cover.png align="left")

Docker Compose is a tool that assists in defining multi-container applications, enabling them to communicate with one another. With Docker Compose, we can run various components of our application in containers as individual services. For instance, our frontend, backend and database will run as a separate service.

To configure these containers, we will use the docker-compose file, which is written in YAML. Within the docker-compose file, we list the components of our application as different services as well as their requirements. With this docker-compose file, we can effortlessly create instances or even tear down our ENTIRE application using just one simple command! Isn't that mind-blowing?! 🤯✨

## ✔ But first ... what are YAML files? 📃

YAML stands for "YAML Ain't Markup Language" (a recursive acronym 😅) and is a human-readable data serialization language, similar to XML and JSON. It enables the transfer of data between applications with different data structures and technologies.

Serialization involves translating and converting data into a standard format, which can be stored or transmitted over a network. YAML is popular for writing configuration files in DevOps tools and applications due to its intuitive syntax.

## ✔ Writing a docker-compose file. ✍️

Let us now explore various configuration options in a Docker Compose file.

1. `version`: In this section, we specify the Docker Compose API version to use when parsing the Compose file.
    
2. `services`: In this section, we list the different services required to run our app, i.e., the various containers that must be running for our application to function properly.
    
3. `build`: If you wish to build your container from a Dockerfile, specify the path to that file in this section.
    
4. `image`: Here, we specify the Docker image from which the container will be built.
    
    **Note:** If the build option is specified, the name provided in this section will be tagged to the created image.
    
5. `container_name`: Here, specify the container name that will be created.
    
6. `command`: This will override the command, i.e., the CMD specified in the Dockerfile.
    
7. `environment`: Here, we specify the environment variables required for the application to function properly. Alternatively, we can use the env\_file option to designate a .env file for our container.
    
8. `depends_on`: This section allows us to specify the services that particularly need other services to start functioning. For example, if we have a Node.js application that requires a MongoDB database, we can indicate this in this section, and the Node.js application will only start once the MongoDB service has begun.
    
9. `expose`: This section defines the ports that Docker Compose will expose from each container.
    
10. `restart`: Define the policy that Docker Compose will apply when a container stops functioning.
    
    * `no`: The default restart policy. Does not restart the container under any circumstances.
        
    * `always`: The policy always restarts the container until its removal.
        
    * `on-failure`: The policy restarts the container if the exit code indicates an error.
        
    * `unless-stopped`: The policy restarts the container irrespective of the exit code but will stop restarting when the service is stopped or removed.
        

## ✔ Let's do a project to better understand docker-compose.🤩

If you wish to follow along, here are some prerequisites:

1. Spin up an ec2 instance.
    
2. Install Docker and docker compose on the EC2 instance.
    
3. Allow users to run Docker without sudo by using this command: `sudo usermod -aG docker user_name` then reboot the instance by executing `sudo reboot`.
    
4. Clone [this](https://github.com/yash91989201/node_docker.git) GitHub repository, which contains the source code application that we will be using in our project, and review the project documentation.
    

After cloning the project cd into `node_docker` directory.

```yaml
version: "3"
# containers are spceified as services
services:

  nginx:
    image: nginx:stable-alpine
    ports:
      - 3000:80
    volumes:
      - ./src/nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
  # below we will add configs that are specific to node-app container
  node-app:
    # path of the docker file to build the container from
    build: .
    image: yash6370/node_docker_app
    volumes:
      - ./:/app
    environment:
      - NODE_ENV=production
      - SESSION_SECRET=thisissomesupersecretsession
    depends_on:
      - mongodb
  # below are the configs that are specific to mongo container
  mongodb:
    image: mongo:latest
    environment:
      - MONGO_INITDB_ROOT_USERNAME=yash
      - MONGO_INITDB_ROOT_PASSWORD=password
    volumes:
      - mongo-db:/data/db
  # below are the configs that are specific to redis container
  redis:
    image: redis

volumes:
  # listing out all the volumes so that other containers can access it
  mongo-db:
  nginx:
```

Above is the required compose file. To quickly spin up each service, simply run the Docker Compose command. Execute the following command to accomplish this:

`docker compose -f docker-compose.yaml -f docker-compose.prod.yaml up -d`

After executing this command, you will get the following output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690908046970/57794342-cbec-44b8-a8de-a38b6a68a4c7.png align="center")

Let's list our containers,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690908106347/9054ef61-d82a-4db2-894d-4618b5bc98b1.png align="center")

Here, we can see that multiple containers have been created, such as node\_docker\_app, mongo, redis, and nginx.

We can also access this application by using ec2 public ip i.e `ec2_public_ip/api/v1/test`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690908206175/584c294f-f3aa-4a78-a745-3e1b9bd52d67.png align="center")

Oh my goodness, docker-compose is incredible! With just a single command, our entire application was up and running in mere seconds! How fantastic is that?!

## **📍** Up Next... ⏭️

Hold on to your hats, folks! In my upcoming blog posts, I'll be explaining more docker-compose options! We'll explore custom networks for container isolation, volumes for data storage, and so much more! So, stay tuned and keep learning, because the excitement never stops!