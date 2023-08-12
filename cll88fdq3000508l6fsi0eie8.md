---
title: "An easy-to-follow guide on Jenkins freestyle project 📜 with Docker🐳."
seoTitle: "An easy-to-follow guide on Jenkins freestyle project 📜 with Docker🐳."
seoDescription: "Hey there, amazing readers! 🎉 Get ready for an incredible hands-on adventure as we  deploy not just one, but TWO fantastic projects using Jenkins"
datePublished: Sat Aug 12 2023 16:29:19 GMT+0000 (Coordinated Universal Time)
cuid: cll88fdq3000508l6fsi0eie8
slug: an-easy-to-follow-guide-on-jenkins-freestyle-project-with-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691857574808/0136aec2-bfdb-47e5-845b-dcb43e84441b.gif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691857702549/cd5ecf14-b0ad-42cb-8fe5-87d7597be78d.gif
tags: docker, jenkins, 90daysofdevops, trainwithshubham, freestyle-jenkins-project

---

## **📍** Introduction:

Hey there, amazing readers! 🎉 Get ready for an incredible hands-on adventure as we deploy not just one, but TWO fantastic projects using Jenkins freestyle job! 🚀🌟

## ✔ Prerequisites:

Before proceeding with this project, ensure that you have the following prerequisites in place.

1. EC2 Instance with Jenkins, Docker, and Docker Compose installed.
    
2. Ports 8000-8005 should be allowed through the EC2 security group.
    
3. Basic knowledge of docker and Jenkins.
    

If you are new to Docker and Jenkins, you can visit my previous blog posts to gain a fundamental understanding of these technologies here &gt; [docker](https://yashraj-jaiswal.hashnode.dev/getting-started-with-docker-for-devops), [Jenkins](https://yashraj-jaiswal.hashnode.dev/a-basic-overview-of-cicd-and-jenkins-for-beginners).

## ✔ Project 01: Deploying todo application.

For the first project, we will be deploying a containerized application using a Jenkins freestyle project.

### 🔸 Step 1: Create a new job. 💼

* Create a new job then, on the next page enter the name of your job and then select freestyle project.
    
* You can optionally add a description for your job.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691850906938/6fbcc759-c423-47ce-8c63-4a634dd566e2.png align="center")
    

### 🔸 Step 2: Add a build step.⛏🪜

* Go to the build step section and choose the "Execute Shell" option. And then paste the following bash script.
    
    ```bash
    if [ ! -d "django-todo" ];then
    	git clone https://github.com/yash91989201/django-todo.git 
    fi
    
    cd django-todo
    docker build . -t django-todo 
    
    # if container is already running remove it
    if [ ! -z "$(docker ps -aq)" ]; then
    	docker rm -f "$(docker ps -aq)"
    fi
    docker run -d -p 8000:8000 --name django-todo django-todo
    ```
    
* After adding the build step save the job.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691852020108/3f1eed9c-04fd-4a26-b256-075d89c9f39a.png align="center")
    

### 🔸 Step 3: Executing our job.⚙️

* After adding the build step, now execute the job by clicking on "Build Now" on the left side.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691852127234/49b85fba-1776-4c99-9a8b-3b3aa0f45d73.png align="center")
    
* Access the output of your build by clicking on the build history. We can see that our build finished successfully.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691853323406/b13f26b5-75cc-4992-bc94-c617cc373ce5.png align="center")
    

### 🔸 Step 4: Access the application.**🌐**

To access the deployed application use the EC2 ip address along with the 8000 port i.e. `ec2_ip_address:8000` . If the project is deployed successfully you will see the following on your screen.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691853392394/cb3684e0-8b7c-4985-b4ce-6f477b4f95b5.png align="center")

You can also interact with the application and add a to-do item.

## ✔ Project 02: Deploying a Django application using docker-compose.

For the first project, we will be deploying a containerized application using a Jenkins freestyle project with docker-compose.

### 🔸 Step 1: Create a job. 💼

* Create a new job then, on the next page enter the name of your job and then select freestyle project.
    
* You can optionally add a description for your job.
    

### 🔸 Step 2: Add a build step.⛏🪜

* Go to the build step section and choose the "Execute Shell" option. And then enter the following bash script.
    
    ```bash
    if [ ! -d "django-compose-app"  ]; then
    	git clone https://github.com/yash91989201/django-compose-app.git
    fi
    
    cd django-compose-app
    
    docker compose -f docker-compose.yaml up -d 
    ```
    
* After adding a build step save the job.
    

### 🔸 Step 3: Creating a docker volume. 💾

Before we execute our job, we need to create a docker volume that our application will be used to store data.

Create a docker volume by executing the following command `docker volume create my_django_volume`

### 🔸 Step 4: Executing our job. ⚙️

* After adding the build step, now execute the job by clicking on "Build Now" on the left side.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691853802298/707accc7-8f1b-4b29-9481-dc8dd25ed624.png align="center")
    
* Let's see the output of our build.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691853866226/6117ccd1-1ca8-4353-b2ea-ab134a398fc4.png align="center")
    

### 🔸 Step 5: Access the application.**🌐**

* To access the deployed application use the EC2 ip address along with the 8000 port i.e. `ec2_ip_address:8001` . If the project is deployed successfully you will see the following on your screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691854503357/bb485607-5307-4044-89e4-aed5c9889d72.png align="center")
    

## **📍** Conclusion: **🎉**

We've done it! We've successfully deployed not just one, but TWO containerized applications with the help of Jenkins 🎉 This is just a freestyle project, but guess what? In our upcoming blogs, we'll dive into creating even more amazing projects using pipelines! Get ready for some serious fun! 😄