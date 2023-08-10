---
title: "👨🏽‍🏫A Basic overview of CI/CD and Jenkins for beginners.⚙️🔄"
seoTitle: "👨🏽‍🏫A Basic overview of CI/CD and Jenkins for beginners.⚙️🔄"
datePublished: Thu Aug 10 2023 15:21:46 GMT+0000 (Coordinated Universal Time)
cuid: cll5b4t2l000m0al5edpy0hda
slug: a-basic-overview-of-cicd-and-jenkins-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691680322207/b9a3a173-3bff-4920-bb38-11cb9e219e2b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691680828227/f2fa55bc-41de-4c16-af87-2331108b7e22.png
tags: devops, jenkins, 90daysofdevops, trainwithshubham, tws

---

## **📍** Introduction:

Get ready for an amazing journey! After mastering Linux, Git, GitHub, and Docker, today we're diving into the thrilling world of CI/CD! And guess what? We'll be learning about an amazing tool that makes implementing CI/CD a breeze! Let's get started!

## ✔ Let's first learn about CI/CD.

CI stands for continuous integration and CD stands for continuous deployment/delivery. This is a methodology or process that helps us to automate and streamline the processes that are involved in a software's development lifecycle i.e. from building a project, testing it and delivering it finally.

### 🔸 Continuous Integration:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691601952240/0e18fbfa-23db-4716-a096-d6580cd90118.png align="center")

This is the stage where developers write code for the software and commit their changes to a distributed version control system. GitHub is one of the most widely used distributed version control systems. Once all the developers have pushed their code to the repository, it triggers an automated build process.

This process involves multiple steps: first, the code is compiled, and then it is executed to identify any compile-time errors. Upon successful completion of this process, the project undergoes testing. If any bugs are discovered during testing, the developers are promptly notified of the issue so they can prioritize fixing it.

This process occurs continuously, meaning that after the developer fixes the bug and pushes it to the repository, the code is built, executed, and tested again.

### 🔸 Continuous Delivery/Deployment:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691602012108/3e4976f5-fce2-41c7-b135-9e58b148070e.png align="center")

After coding for a feature is done and the changes are tested, the code is deployed. Continuous development or delivery aims to rapidly deploy the changes to the production environment, where they are released to the users.

In Continuous Delivery (CD), several steps are followed in which the application code is first subjected to unit tests, followed by integration. Once the integration part is complete, final testing is conducted. After all these processes have been completed, the last step, deployment, is carried out.

The difference between deployment and delivery lies in the level of automation involved. In deployment, all steps are automated, eliminating the need for human intervention. In contrast, delivery involves manual production deployment carried out by humans.

## ✔ How does Jenkins fit into this scenario?

Jenkins is an open-source tool that allows us to implement CI/CD processes efficiently and automates every step in these processes. Being written in Java, Jenkins can run on any platform, whether it be Mac, Windows, or Linux. Jenkins was developed by Sun Microsystems in 2004 and was initially named Hudson.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691603532346/6f195317-9d8f-4959-b400-97dbc10b548d.png align="center")

Jenkins supports the concept of pipelines, which allows you to define the entire end-to-end software delivery process as code. This includes building, testing, and deploying applications. Pipelines can be scripted using a domain-specific language called Groovy, providing flexibility and customization.

## ✔ Plugins in Jenkins:

One of the primary reasons Jenkins is widely used as a CI/CD tool is due to its extensive plugin ecosystem. As an open-source project, numerous plugins are publicly available for everyone to utilize.

Plugins are extensions that enhance the functionality of Jenkins. They can add support for various version control systems, build tools, testing frameworks, notification services, and more. Jenkins has a rich ecosystem of plugins that can be installed and configured to meet specific needs.

## ✔ Jenkins Terminologies:

### 🔸 Job

A job is a specific task or set of tasks established to automate parts of the software development lifecycle or the entire SDLC process. It may involve multiple steps, such as retrieving code from GitHub, building the code, executing it, and conducting tests. Types of jobs include free-style jobs, pipeline jobs and multi-branch pipeline jobs.

### 🔸 Build

A build is a running instance of a job i.e. when we execute a job it creates a build and all the tasks specified within the job are run in a build. Jenkins keeps track of the status of the build and its log report. Successful builds proceed to the next step while failed builds are notified to the user.

### 🔸 Node

A node is an individual machine that handles the execution of jobs. A node can be a physical machine, a virtual machine or even a docker container.

### 🔸 Master node

The master node is the primary Jenkins server that schedules and distributes the tasks of executing various jobs to slave nodes. If no slave nodes are available, the master node handles the execution of all jobs. Additionally, the master node monitors the overall system health and hosts a web interface, allowing users to create jobs, manage plugins, and view job reports.

### 🔸 Slave node

Also known as worker nodes, these machines are connected to the master node. They handle the actual execution of jobs as instructed or scheduled by the master node. This strategy of dividing jobs enables parallel execution and increases efficiency. Labels can also be added to worker nodes to indicate that they will handle the execution of specific tasks only.

### 🔸 Executor

Executors are responsible for executing jobs on a node. Each node possesses a collection of executors, representing the node's processing capacity. They carry out tasks assigned by the master node and execute them. Executors enable the concurrent execution of multiple jobs on a single node and are configured for each agent. When setting up a new agent, you can specify the number of executors the agent should have.

### 🔸 **Jenkinsfile**

If we want to create a pipeline job then we can use a Jenkinsfile to specify all the steps that we want our pipeline to execute. To specify steps in a Jenkinsfile we use a scripting language called Groovy.

## ✔ Let's create a freestyle project in Jenkins:

1. Go to Jenkins dashboard and click on `New item`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691679216195/4466a688-aa35-49d5-8acb-16785c88e88b.png align="center")
    
2. Enter the name of your job and choose the `Freestyle Project` option.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691679359747/d1d93aa5-25c9-40b0-975a-3a0d2a50bfcb.png align="center")
    
3. Go to the build step section, choose the `Execute shell` option and enter a Linux command that you want to execute. In this example, we will use `echo hello world` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691679431184/32215739-9a60-461a-8530-0bd87df55ad5.png align="center")
    
4. After saving the configuration for your helloworld job we can build it using the Build Now option.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691679612078/24e8718e-fffc-459f-a059-185fe4add23b.png align="center")
    
    You can see the build running here
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691679663633/61ebf6ec-1910-46d2-93fc-a52ace316092.png align="center")
    
    Click on the green tick icon and you will see information about your build.
    
    In the output, we can see that the command `echo "hello world"` was executed, and hello world was printed on the screen. Then the build finished with a SUCCESS message.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691679759100/ee0e884b-16fa-4e50-ad42-a59f220b236f.png align="center")
    

## **📍** Conclusion:

"Hello world" is just a simple example, but guess what? In my upcoming blog posts, I'll be doing many amazing projects using Jenkins. So, stay tuned and keep learning, because it's going to be a thrilling adventure!