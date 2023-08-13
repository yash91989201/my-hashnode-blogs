---
title: "🚀🚀Jenkins CI/CD project using GitHub web hooks. 🪝🏗️"
datePublished: Sun Aug 13 2023 16:14:52 GMT+0000 (Coordinated Universal Time)
cuid: cll9ncnrt000i0aiecghscf1r
slug: jenkins-cicd-project-using-github-web-hooks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691943191047/a27bdb1b-6834-4923-9389-ab70004cd5bb.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691943249542/57b5aa33-749a-4bf0-8dc5-5d10490366c2.png
tags: docker, jenkins-devops, github-webhook, 90daysofdevops, freestyle-jenkins-project

---

## 📍 Introduction:

Hello readers! 👋👋 Welcome to today's blog, where we will explore a fascinating concept called webhook and learn how to utilize its functionality by deploying our project. Actually, the deployment will be done automatically😏🤩, want to know how🤔? Let's begin by first understanding what a GitHub webhook is and how it works.

## ✔️ What is a GitHub webhook?

GitHub webhook is a feature that can be used to automate aspects of our development workflow. With GitHub webhooks, we can set up various responses to events occurring in our GitHub project repositories. These events include pushing code to a branch, opening/closing a pull request, or creating a release.

For example, if we want the changes to be deployed whenever code is pushed to a certain branch ( which allows us to test our modifications immediately ) we can implement that behavior with GitHub webhooks.

## ✔️ How GitHub Webhooks Work?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691941678541/7b94c235-679d-452a-a046-ca5ff5ad2144.png align="center")

When creating a webhook, we need to specify the types of events our webhook should respond to and provide a payload URL. Once these settings are configured, our webhook is created.

Now, in our repository, if any of the specified events occur, the payload URL will be called using a POST method, and its request body will contain all the information about the event. We can then use this information to perform actions accordingly.

## ✔️ Jenkins freestyle project using GitHub webhooks.

Now that we understand how GitHub webhooks function, let's create a freestyle project in Jenkins that utilizes GitHub webhooks to initiate an automatic build when code is pushed to the master branch.

If you are unfamiliar with creating a freestyle project in Jenkins, feel free to check out my [previous blog post](https://yashraj-jaiswal.hashnode.dev/an-easy-to-follow-guide-on-jenkins-freestyle-project-with-docker), which provides an in-depth explanation of how to create a freestyle project in Jenkins.

If you would like to follow along with this project, ensure that you have the following prerequisites in place.

1. EC2 instance with Jenkins and Docker installed.
    
2. 8000 port allowed through security group inbound rule.
    
3. ubuntu user must be added to the Docker group.
    
4. Fork this [GitHub project](https://github.com/LondheShubham153/node-todo-cicd) into your account.
    
5. Familiarity with configuring Jenkins freestyle projects.
    

### 🔸Step 1: Creating a freestyle project.

Let's begin by creating a freestyle project and providing an appropriate description.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691931328669/d519eaad-1b4d-4110-a379-b583fc99b231.png align="center")

### 🔸 Step 2: Adding GitHub repository.

Now, we will provide the link to our GitHub repository and the branch from which our code will be pulled and deployed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691931754844/60ef8b6b-ce82-4d36-841a-5d6a8306cd71.png align="center")

### 🔸 Step 3: Configuring GitHub WebHook.

* For our GitHub webhook to function, we first need to install a plugin on our Jenkins server.
    
* Go to Manage Jenkins &gt; Plugins &gt; Available Plugins &gt; Search for 'GitHub Integrations' and then click on 'Install without restart'.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691937463104/2715a3c3-2fea-4e09-852b-96e9fcf7e797.png align="center")

* Under the 'Build Triggers' section select 'GitHub hook trigger for GITScm polling'
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691936111969/0c6377c5-86f1-44a1-b8b8-364d8bc69719.png align="center")

* Next, navigate to the forked repository, access the settings page, and locate the 'Webhooks' section. Add the payload URL, and then set the content type to 'application/json'.
    
* Then click on `Add webhook` to save your webhook.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691936561854/a94c8801-6b65-4200-92b0-06e196cebdf4.png align="center")

* Make sure there is a green tick left to the added webhook, this indicates that the webhook has been added successfully.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691936244405/47652025-b90b-41b4-bfa2-819c49df9918.png align="center")

* If you don't see the green tick, there might be an error. To find what went wrong, click on the `Edit` button below the webhook and navigate to the `Recent Deliveries` section. Here, you can identify the probable cause of the error.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691938092033/187b7cc5-582c-474d-bea1-7b16ff2c3154.png align="center")
    

### 🔸 Step 4: Adding a build step.

Now in the build step section add the command that will build your project. In our case, we can add a single docker compose command to spin up our project within a container i.e. `docker compose up -d`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691936044041/a338b34a-4e4e-409a-b020-3fa8bc718b9c.png align="center")

### 🔸 Step 5: Triggering build by changing source code.

Now for the interesting part, triggering a build with a push event on the master branch.

* Make some changes to your forked repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691938574509/edce420e-494b-46b1-aa85-a088a9f4cf63.png align="center")
    
* After your commit and push your changes you will see a build job has been triggered and our application has been deployed successfully, all this happened automatically with the power of GitHub webhooks.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691938703131/77036e3e-1eac-4b3a-bad6-9c16613ba8b2.png align="center")
    

### 🔸 Step 6: Let's see the deployed application.

Go to the ec2 instance's ip address with port 8000 to see the application running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691938865515/059a5a43-aad3-4fe2-8d0a-d26183bcf61c.png align="center")

## 📍 Conclusion:

By utilizing the concept of webhooks, we can streamline our development process. This enables us to quickly see our changes reflected, and instantly accessible through a URL, allowing us to test our code and iterate or correct it as needed.

In the future, our blog posts will explore more complex Jenkins ideas, helping us understand its detailed features and discover additional opportunities in software development. Till then keep learning and upskilling.

Thanks for reading this blog! I hope you learned something useful. Stay tuned for more easy-to-understand DevOps concepts by following me on:

Hashnode: @[Yashraj Jaiswal](@yashraj-jaiswal)

LinkedIn: [linkedin.com/in/yashraj-jaiswal-91989201s](https://www.linkedin.com/in/yashraj-jaiswal-91989201s/)