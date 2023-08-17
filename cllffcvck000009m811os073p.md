---
title: "👨‍🏫 Introduction to Jenkins Pipeline for Beginners."
seoTitle: "Jenkins Pipeline Basics: Beginner's Guide"
datePublished: Thu Aug 17 2023 17:17:42 GMT+0000 (Coordinated Universal Time)
cuid: cllffcvck000009m811os073p
slug: introduction-to-jenkins-pipeline-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692292019907/86741a63-01ba-414f-868a-8c794703800e.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692292648446/a166275b-c119-45f5-9fd7-dbff4a8b738e.png
tags: devops, jenkins, 90daysofdevops, trainwithshubham, jenkins-declarative-pipeline

---

## 📍 Introduction:

Hello readers! 🎉 Get ready to learn about Jenkins pipeline 🚀 With pipelines, automating integration and deployment in a project has never been easier! 💪 Not only that, but we'll also learn about the Declarative pipeline in Jenkins and get our hands dirty by creating our very own pipeline! 🤩 Let the adventure begin!

## ✔️ What is a pipeline?

A pipeline contains all the steps that are required to deploy a project. But a pipeline is an automated way of executing those steps. It performs all the steps for continuous integration and continuous delivery of a software application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692292224484/4b2fd093-6871-4b30-87a8-6a374ed96a97.png align="center")

The pipeline streamlines the process of building, testing, and deploying software, leading to quicker development cycles, fewer human errors, and enhanced collaboration among developers.

## ✔️ Declarative pipelines in Jenkins.

Declarative pipelines in Jenkins offer a modern approach to scripting your pipeline as code. Within a `Jenkinsfile`, all the steps in your pipeline are specified within blocks, accompanied by other configurations. This file can now be stored in your project repository for seamless integration.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692292405450/4fcdc69f-5b1b-4233-8557-b4b2a28663ed.png align="center")

A declarative pipeline offers a straightforward syntax, containing various sections that enable us to define each step in our pipeline individually. Let's examine the declarative pipeline syntax.

1. `pipeline`: All the steps and configuration of a pipeline must be enclosed within a pipeline block.
    
2. `agent`: In the agent section we can specify in which node the pipeline will be executed. We can also specify different agents for different stages of our pipeline, this depends on where we place our agent section.
    
3. `stages`: In this section, we defined the different stages that our pipeline will execute.
    
4. `stage`: Within this section, we define a single stage in a pipeline like pulling code from GitHub, building code, testing etc.
    
5. `steps`: This section allows us to specify the steps that we want to execute for a stage.
    

## ✔️ Let's create a pipeline.

To create a pipeline we will first create a new job and select the "Pipeline Project" option.

Then in the pipeline section paste the following code, we can also put this in a file named 'Jenkinsfile' within our project and pull the code from GitHub:

```plaintext
pipeline {
    agent any 
    stages {
        stage('Pull code') {
            steps {
                sh 'echo Pull code from github'
            }
        } 
         stage('Build project') {
            steps {
                sh 'echo build project successful.'
            }
        }
         stage('Test') {
            steps {
                sh 'echo Execute all the test cases.'
            }
        }
         stage('Deploy') {
            steps {
                sh 'echo Deploy the project'
            }
        }
       
    }
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692289322784/ad1ea8ff-8b61-415d-a8e0-ac8864347ab3.png align="center")

On executing the pipeline we will get the following output.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692289283217/b7f82593-5666-46a0-9598-23af7da93020.png align="center")

In the below image, we can see the steps within our stage getting executed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692290877924/96fca63c-3c1c-4f77-a9f2-0094641d0282.png align="center")

One of the advantages of using a pipeline is that if a stage fails, we can resume from that specific stage rather than running the job from the beginning, which is not possible in a freestyle project.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692291293045/9d933d74-7522-4aa9-97dd-2e019a627824.png align="center")

## 📍 Conclusion:

In the example above, we've just showcased a basic declarative pipeline in Jenkins! You won't want to miss my upcoming blog posts, where I'll be creating some fantastic pipelines to deploy projects! So stay tuned, and keep learning!