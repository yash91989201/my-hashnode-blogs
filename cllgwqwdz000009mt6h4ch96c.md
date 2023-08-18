---
title: "Jenkins Declarative Pipeline with Docker.✨✨"
datePublished: Fri Aug 18 2023 18:12:16 GMT+0000 (Coordinated Universal Time)
cuid: cllgwqwdz000009mt6h4ch96c
slug: jenkins-declarative-pipeline-with-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692382312482/de86ce7c-ef16-4670-af1d-9cb44692efdb.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692382297892/15a3bb89-2e28-4b41-8af0-995725463444.png
tags: docker, devops, jenkins, 90daysofdevops, trainwithshubham

---

## 📍 Introduction:

Hi there amazing readers, in the [previous blog](https://hashnode.com/post/cllffcvck000009m811os073p), we learned about the Jenkins declarative pipeline and its implementation using a project. Today, we will explore how to integrate Docker into our pipelines.

## ✔️ Prerequisites:

Before we move forward make sure that you have the following prerequisites in place:

1. Basic understanding of docker and Jenkins pipeline.
    
2. The different types of sections used in a declarative pipeline. Refer to [this section](https://yashraj-jaiswal.hashnode.dev/introduction-to-jenkins-pipeline-for-beginners#heading-declarative-pipelines-in-jenkins) of my previous blog to get a quick understanding.
    
3. Docker installed and configured for Jenkins user (not required when the pipeline is executed by the root user).
    

## ✔️ Initial Steps:

Here are the steps you can follow to ensure that your environment is correctly configured.

```bash
# installing docker
sudo apt-get update
sudo apt install docker.io
# configuring docker access to the user
usermod -aG docker ubuntu
```

## ✔️ Integrating docker within a pipeline:

### 🔸 Task 1:

For the first task, we will be creating a pipeline with the following steps: pull code, test, build image, and deploy the container.

For this first, we have to create a new job with a pipeline project selected. Then use the following script for the pipeline.

```bash
pipeline{
    agent any
    stages{
        stage("Code pull from github"){
            steps{
                 git url: 'https://github.com/yash91989201/django-todo-cicd', branch: 'develop'
            }
        }
        stage("Code testing"){
            steps{
                sh 'echo "Code testing success."'
            }
        }
        stage("Build docker image"){
            steps{
                sh 'docker build . -t django-todo-ci-cd'
            }
        }
        stage("Deploy code"){
            steps{
                sh 'docker run -itd --rm --name django-todo-ci-cd django-todo-ci-cd'
            }
        }
    }
}
```

On running the job the first time, you will see that all the tasks are completed and your container will be running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692380460342/c8faa019-d4a3-4a5d-869b-03a016ccf93b.png align="center")

But on running the job a second time we will face an error. Let's see what is causing the error.

In the below output, we can see that we get an error that the port is already in use. This means that the container created on the first job execution has been allotted that port and cannot be used by any other container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692380494242/d2e59b81-be00-48c7-a57d-b3f2d2baab3f.png align="center")

Let's proceed to Task 2 to explore the solution for the above issue.

### 🔸 Task 2:

To tackle the problem of port being already allocated we can make use of docker-compose. For this first locate the running container and remove it.

Now make following

changes in the pipeline steps:

```bash
pipeline{
    agent any
    stages{
        stage("Code clone"){
            steps{
                 git url: 'https://github.com/yash91989201/django-todo-cicd', branch: 'develop'
            }
        }
        stage("Code test"){
            steps{
                 sh 'echo "Code testing successful." '
            }
        }
        stage("Deploy code"){
            steps{
                sh 'docker compose up -d'
            }
        }
    }
}
```

Docker compose will automatically build our image and deploy it. It will also handle starting and stopping of our containers, it will do so only when something is changed.

Now run the pipeline again and you will be able to open the website deployed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692381370547/c90375eb-eeb7-43ec-8fe3-725e4e121adf.png align="center")

## 📍 Conclusion:

In this article, we explored how to integrate Docker into Jenkins declarative pipelines, enabling more efficient and streamlined workflows. By using Docker and docker-compose, we resolved issues related to port allocation, making the pipeline more robust and flexible. With this knowledge, you can now implement Docker within your own Jenkins pipelines for improved project management and deployment.

In the next blog, we will set up a master and slave configuration for executing our jobs. If you learned something new today, please share your experiences in the comments.