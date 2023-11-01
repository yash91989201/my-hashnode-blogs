---
title: "Hosting a  static website on AWS using  S3 bucket and CI/CD Pipeline."
seoTitle: "Hosting a  static website on AWS using  S3 bucket and CI/CD Pipeline."
datePublished: Wed Nov 01 2023 16:08:41 GMT+0000 (Coordinated Universal Time)
cuid: clofycunw000009l27jhjdwsb
slug: hosting-a-static-website-on-aws-using-s3-bucket-and-cicd-pipeline
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698854777812/e19e59fa-cfb0-4803-9ede-5236b03a907c.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1698854849569/658def20-b3ef-42df-9246-a7c9a123756e.png
tags: cloudfront, reactjs, devops, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

Hello readers! In today's AWS hands-on project, we will deploy a simple React website on S3 and distribute it using CloudFront. Additionally, we will explore how to automate the entire deployment process using CI/CD to deploy our project when code is pushed to our repository.

## ✔️ AWS hands-on practice

For this hands-on practice if you want to follow along, here are the following pre-requisites that you need to have in place:

1. GitHub account connected to AWS.
    
2. Fork [this repository](https://github.com/yash91989201/project_hoobank).
    
3. Basic knowledge of Code build, code pipeline and S3 bucket.
    

### 🔸 Task 1: Setting up the S3 bucket

First, we will set up an s3 bucket to store our react website code. Follow the below steps to set up the s3 bucket.

1. Go to the S3 Buckets page and then click on Create a Bucket.
    
2. Then on the next page fill in the following details.
    
3. For the bucket name choose any name you want or if you have a domain purchased, you can enter it here.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698807556451/35285291-429e-438b-9bc8-b94c369dc249.png align="center")
    
4. Block all public access to the s3 bucket, this is checked by default but make sure you don't uncheck it because we will be using Cloud Front to provide users access to our website.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698807675620/01985c20-11b0-4b4c-8915-156c5c734eef.png align="center")
    
5. Enable bucket versioning.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698807758121/68e08892-f95a-4d4e-a4d9-4681d2c7035f.png align="center")
    
6. Now go to the bottom and click on Create Bucket.
    
7. After the bucket has been created go to its properties scroll to the bottom and edit `Static Website Hosting` Settings. Also for the index page enter index.html
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698808011410/6061bf13-c4bf-4163-80a9-183063feacb9.png align="center")
    
8. Save the changes and now your s3 bucket is set up.
    

### 🔸 Task 2: Using Cloud Front to serve our website

Follow the below steps to set up the cloud front so that we can serve our website using the S3 bucket that we created in the previous step.

1. Go to the cloud front dashboard and click on Create distribution.
    
2. For the origin settings select the s3 bucket that we created previously.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698809284923/e8e79c93-0fdb-44c5-9c91-a0d3a00305fa.png align="center")
    
3. Select Legacy Access Identities for the Origin access and click on Create new OAI if you don't have one already. Then also select "Yes, update the bucket policy", this will update the bucket policy to work with the cloud front.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698809374068/f7a1c932-50ca-43aa-add9-b7bfb1c3555b.png align="center")
    
4. Select Redictet HTTP to HTTPS in the Viewers section.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698809529435/af4462c7-63a2-411c-91cf-f1b9af5258fa.png align="center")
    
5. Enable Web Application Firewall.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698809767365/dafc92f8-9616-43c7-a0e0-13977450b948.png align="center")
    
6. You can also use an SSL certificate from ACM to secure your website.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698809675614/8fbc2e4a-36c0-4227-abfb-28d68496e5bc.png align="center")
    
7. Keep other options as default and Create distribution. It will take a couple of minutes for our distribution to be created.
    
8. After the distribution is created you will see the status as enabled.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698810018148/50571801-80be-4001-aff1-881af7b351d6.png align="center")
    

### 🔸 Task 4: Automating website deployment

Now that our distribution is created we can create a CI/CD pipeline to automatically deploy our website code to the S3 bucket.

First, we need to create a build project on AWS Code build.

1. Navigate to the CodeBuild dashboard and click on "Create build project."
    
2. Give your build project a name.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698848979483/4b89a424-a3b3-4480-974d-c7a532a5bcd3.png align="center")
    
3. Select your GitHub repository as the primary source.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849022788/3b764487-df3d-4bf0-aea3-7310e27b4e39.png align="center")
    
4. Setup the environment section as follows
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849160784/d3ab896a-e967-4652-9289-a65651c2c0b5.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849173185/f3c37480-9d71-4f59-99d3-52139e84516e.png align="center")
    
5. Setup artifacts as follows, this will put the build file in the s3 bucket. Here select the s3 bucket that you have created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849344679/753f24ce-ce37-4aae-a4b4-8c91973c9d6b.png align="center")
    
6. Scroll to the bottom and click on "Create Build Project."
    
7. After the build project has been created, you can run it and observe that the build files are output in the S3 bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849599134/38c6bcc0-0bdd-458a-81b7-4bbc511a7cc4.png align="center")
    

Second, we need to create a pipeline to look for changes and start the build when there is a push in the repository.

1. Navigate to the CodePipeline dashboard and click on "Create Pipeline."
    
2. Give a name for your pipeline and then click on next
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849884849/7902fbf4-89a3-4818-b54b-b2b1f21c78d4.png align="center")
    
3. For the source stage select GitHub and then select the repo that you just forked.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849937492/80741f41-bd02-4517-847e-2a0da5ce80ec.png align="center")
    
4. In the build stage select the build project that we created in the previous step.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698849971306/f8d3251a-55d7-4e3f-9f1f-a9014df3d11e.png align="center")
    
5. Now, skip the deployment stage, as the build project will automatically place the build output in the specified S3 bucket, according to the buildspec.yml file in the repository.
    
6. Now, click on "Create Pipeline."
    
7. After making changes to your repository, the pipeline will automatically run and push the updated code to the S3 bucket.
    

### 🔸 Task 5: Accessing website

Now you can use the `Domain Name` is shown in the cloud front dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698853498307/e2fb436c-8d56-4bab-8c8b-52a2ccbfa5c5.png align="center")

## 📍 Conclusion

In conclusion, we have successfully hosted a static website on AWS using an S3 bucket and CloudFront distribution. We also automated the deployment process using a CI/CD pipeline with CodeBuild and CodePipeline. This setup allows for seamless updates to your website whenever changes are pushed to the repository, ensuring a streamlined and efficient deployment process.

Hey there! I hope you found this blog helpful. If you did, please feel free to give this blog a like and share it with others who might find it useful too. If you want to learn more about DevOps and cloud, feel free to connect with me on [**LinkedIn**](https://www.linkedin.com/in/yashraj-jaiswal-91989201s/)! 😊