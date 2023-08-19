---
title: "Jenkins interview questions for beginners.🧐"
seoTitle: "Jenkins interview questions for beginners.🧐"
datePublished: Sat Aug 19 2023 17:10:29 GMT+0000 (Coordinated Universal Time)
cuid: clli9zal6000608l2etgt764c
slug: jenkins-interview-questions-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692464844989/a9e0dbac-6744-4022-b1ed-b07b697a7ee3.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1692465013814/9753c82b-f337-4fd8-bbeb-1ad2cf1fee3c.png
tags: devops, jenkins, 90daysofdevops, trainwithshubham, jenkins-interview-questions

---

## Introduction:

After writing multiple blog posts on Jenkins, pipeline projects, and integrating pipelines with Docker steps, today's blog will focus on Jenkins-specific questions related to Docker that can be used during a DevOps Engineer interview.

## Let's get started with the questions.

### What’s the difference between continuous integration, continuous delivery, and continuous deployment?

**Continuous integration** involves the process that is concerned with the development side of the project. In continuous integration, the developer writes code and pushes it to the repository, which triggers a series of steps that involve building the code, executing it, testing, and notifying the developer of success or any potential errors. This means any errors that can occur in the software are caught, and in this way, developers can implement a solution for the issues.

**Continuous delivery** focuses on providing customers with new features of software once coding and testing have been completed. The deployment is carried out manually to maintain thorough control over the processes.

**Continuous deployment** advances the concept of continuous delivery by automatically deploying the code to production once all stages of the pipeline have been completed.

### Benefits of CI/CD.

Some of the most prominent benefits of implementing a ci/cd pipeline for a project are as follows:

1. Faster release cycles.
    
2. Improved quality.
    
3. Increased collaboration.
    
4. Increased efficiency.
    
5. Greater flexibility.
    

### What is meant by CI-CD?

CI/CD stands for Continuous Integration and Continuous Deployment. It is a software development practice that involves automatically building, testing, and deploying code changes to production as soon as they are committed to version control. CI/CD aims to identify and resolve errors as swiftly as possible, enabling quicker and more dependable releases.

### What is Jenkins Pipeline?

Jenkins Pipeline is a set of tools in Jenkins that helps create, build, test, and deploy code changes in a continuous delivery process using a Jenkinsfile stored in the code's source control. It automates and streamlines the build and release process, offering features like running tasks at the same time, managing different paths, and handling errors.

### How do you configure the job in Jenkins?

Here are the steps to configure a job in jenkins:

Step 1: Click on "Create an item" on the dashboard page.

Step 2: On the next page give a name for the job, select the job type and then proceed.

Step 3: Set the required options on the given fields and then save the pipeline.

### Where do you find errors in Jenkins?

When we build jobs we can find the errors in the console output, which we can access from the build history section on the job page.

### In Jenkins how can you find log files?

We can find the log file here &gt; /var/log/jenkins/jenkins.logs

### How to create a continuous deployment in Jenkins?

We can create a continuous deployment in jenkins by automating the process from pulling the code from Git Hub to deploying the project. This can be achieved by using GitHub webhooks, it works in the following way code is committed to the code management repository &gt; code is automatically picked up by jenkins &gt; code is built &gt; executed &gt; perform testing &gt; if testing is success then start the deployment process on the production server.

### How to build a job in Jenkins?

To build a job in jenkins we just use the Build Now button on the ui this starts the execution of a job.

### Why do we use a pipeline in Jenkins?

Pipeline in Jenkins is a very powerful and flexible way to automate our continuous integration and deployment workflow. Within a pipeline, we can specify different steps to fulfill our workflow requirements.

Separating our tasks into different steps gives us a clear and concise overview of a pipeline. It is advantageous in the sense that if a specific stage in a pipeline fails, we can just resume that step directly rather than redoing the processes altogether, which is usually the case in a freestyle project.

### Is Only Jenkins enough for automation?

Jenkins is a powerful tool for automation, but it may not be sufficient for all automation needs. The best approach is to evaluate your automation requirements and choose the tools and technologies that best meet your needs.

### How will you handle secrets?

For sensitive data that should not be exposed, we can store that secret in Jenkins Credentials Manager. We can then access the secret within our pipeline by using the withCredentials() step, which injects the secret into our pipeline during execution and only where it is required.

### Explain diff stages in CI-CD setup.

The different stages in a ci/cd setup may vary differently according to the project requirement, but these steps are commonly used in every project.

1. Code checkout: This step involves getting code from a source code management tool such as GitHub, GitLab, or Bitbucket.
    
2. Code build: In this stage, the code is executed and the project is started.
    
3. Testing: Upon implementing various test cases according to the project requirements, the code undergoes testing for errors. If the code passes this stage, the pipeline proceeds; however, if any errors are encountered, the pipeline is terminated and the developers are notified of the error.
    
4. Staging: For projects that require manual testing the project is deployed on a staging url commonly known as UAT (user acceptance testing)
    
5. Deployment: After completing all the steps and thoroughly testing the code, the project is ready for deployment on production servers. At this stage, the project is deployed and made accessible to users.
    

### Name some of the plugins in Jenkin.

Some of the most commonly used Jenkins plugins include Docker, Git, maven, blue ocean, ant, gradle, credentials and SonarQube. These plugins are essential in a Jenkins pipeline and are widely utilized.

## Conclusion:

I hope you learned something new from today's blog. If you have any significant questions related to Jenkins that might be helpful for a DevOps interview, please feel free to mention them in the comments section. This will greatly benefit everyone.