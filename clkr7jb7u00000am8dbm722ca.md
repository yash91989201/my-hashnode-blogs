---
title: "Let's run a docker container using Dockerfile."
seoTitle: "Running a docker container using Docker file - devops project"
seoDescription: "Discover Docker containers! Run Python apps, expose ports, create images with Dockerfile. Master containerization now!"
datePublished: Mon Jul 31 2023 18:32:17 GMT+0000 (Coordinated Universal Time)
cuid: clkr7jb7u00000am8dbm722ca
slug: lets-run-a-docker-container-using-dockerfile
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690828078865/ad7b239f-7fa1-4975-9e2c-6d3b9a4d3d07.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690828301080/3bc3341f-fc32-4b6e-bce2-26929828fe51.png
tags: docker, devops, 2articles1week, 90daysofdevops, trainwithshubham

---

Hello readers!! In this amazing blog, we're going to dive into the thrilling world of Docker containers! 🚀 Get ready to run a Python application inside a container and access its amazing services by exposing ports! 🌟 And guess what? The cherry on top is that we'll be using a Dockerfile to create an image and then run a container from it! Let's get started! 🎉

If you are new to Docker, you can acquire a basic understanding by reading my previous blog post [here](https://yashraj-jaiswal.hashnode.dev/getting-started-with-docker-for-devops).

## **📍** Hmm... What's a Dockerfile? 🤔

A Dockerfile is a text document containing all the commands a user might execute on the command line to assemble an image. Docker can automatically build images by reading instructions from a Dockerfile. To write a Dockerfile, we need to follow a specific pattern, i.e., `INSTRUCTION argument`. Docker then uses these instructions to assemble the image layer by layer.

Here are some of the basic instructions that we will be using in our Dockerfile:

1. `FROM`: a docker file must start with a FROM instruction because for an image, firstly we will need a base image. A base image is a starting point or an initial step for the image that we finally want to create.
    
2. `WORKDIR`: This instruction specifies the folder within the container where the application code will be stored.
    
3. `COPY`: Use this instruction to copy the application code into the container: Utilize the `COPY` instruction to transfer the application code into the container, ensuring it is stored in the specified `WORKDIR`.
    
4. `RUN`: Any commands that you want to execute during the image creation process should be specified using this instruction. Typically, RUN is used to install packages required by our application.
    
5. `CMD`: To execute a command when the container starts, use the CMD instruction. This will enable us to run our application as soon as the container begins operation.
    

## ✔ First, we run the project without Docker.

Running the project locally allows us to better understand the project's requirements, which will be beneficial when writing the Dockerfile for creating the Docker image.

If you wish to follow along, here are some prerequisites:

1. Spin up an ec2 instance.
    
2. Install Docker on the EC2 instance.
    
3. Clone [this](https://github.com/shreys7/django-todo.git) GitHub repository, which contains the source code application that we will be using in our project, and review the project documentation.
    
4. Install pip by executing `sudo apt install python3-pip`
    
5. Install Django by executing `pip install Django`
    

After running the project, I realized that some changes need to be made for you to access the running application on the EC2 IP.

Make the following changes in the `django-todo/todoApp/settings.py` file , set the `ALLOWED_HOSTS` setting to \* , like this &gt; `ALLOWED_HOSTS=['*']`

Now, execute these commands to initialize the database, seed it with some data, and subsequently launch the server.

```bash
python3 manage.py makemigrations
python3 manage.py migrate
# this will run the application and serve it on port 8000
python3 manage.py runserver 0.0.0.0:8000
```

After the server runs, you can see the following output, we can see that it is accepting requests and serving appropriate responses:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690823126201/a30d3047-0fbb-4ed6-8660-1f93171b1b38.png align="center")

Access the application by using the ec2 ip on your browser `ec2_public_ip:8000` , you will see the following webpage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690823201506/393c55c3-9e61-47e8-a0a6-b9cd5c2e0d1d.png align="center")

## Now let's containerize this application: 🥳

To run this application, we need to create a Dockerfile containing the necessary steps, which will allow Docker to generate an image from it.

Here is the Dockerfile for creating an image for this application:

```dockerfile
FROM python:3.8-slim-buster
WORKDIR /app
COPY . .

# run commands while the image is being created
RUN pip install --upgrade pip
RUN pip install Django
RUN python3 manage.py makemigrations
RUN python3 manage.py migrate

# This command will run when the container starts
CMD ["python3","manage.py","runserver","0.0.0.0:8000"]
```

1. **Build Docker image:** To build the docker image run the following command `docker build -t todo-app /path/to/Dockerfile` .After running this command you will see the following output:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690825564150/5f05537d-c1ea-45dc-bab2-02c52727e674.png align="center")
    
    Here we can see the steps being added as a layer in the image
    
2. `Run the container:` To run the container just execute `docker run -d -p 8000:8000 --name todo-app todo-app`. The "-d" option stands for "detached." This will run the container in the background and display the container ID, preventing logs from appearing on the screen.
    
3. **Let's peek inside the container**: to see inside the container execute this command `docker logs -f todo-app` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690826261508/ccfa3d05-d26a-4315-86a8-62ae5335705c.png align="center")
    

We can also access the application on the browser by using the ec2 public ip:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690826029321/84ed1711-84c1-48e5-807a-763c50f872b3.png align="center")

## **📍** What's next ..... docker-compose

![](https://varchitectthoughts.files.wordpress.com/2016/01/625955-whats-next-meme.jpg?w=257 align="center")

We are just getting started! While Dockerfile is fantastic for creating docker images, imagine those moments when we need to create MULTIPLE containers - it'd be such a hassle to run them individually with the docker run command. But guess what? We can make running containers a breeze using docker-compose! It's like magic, allowing us to create and destroy multiple containers with just ONE command! How cool is that?!

In my upcoming blog, I'll be explaining how to use docker-compose to effortlessly manage MULTIPLE containers like a pro! Get ready to be amazed! 🤩🚀

I hope you learned something new today. If you enjoyed reading this blog, please share what you found fascinating about Docker and any suggestions for improving my blog would be greatly appreciated.