---
title: "🏗️ Introduction to AWS cloud fundamentals for beginners ☁️"
seoTitle: "🏗️ Introduction to AWS cloud fundamentals for beginners ☁️"
datePublished: Fri Sep 29 2023 03:39:39 GMT+0000 (Coordinated Universal Time)
cuid: cln422hn1000109mm6orw1lns
slug: introduction-to-aws-cloud-fundamentals-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695610071612/066890bd-2b01-4065-be4f-11037f113a3a.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695610138619/52a0ba33-d453-40c0-a29f-0ccc91eb2e82.png
tags: aws, devops, iam, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

After mastering Kubernetes, we're about to dive headfirst into the incredible world of Amazon Web Services (AWS)! 🎉 In the upcoming days, we'll be exploring all the amazing AWS concepts, and guess what? We'll be doing hands-on practice at the end of each blog! 🚀 So, buckle up and let's get started on this thrilling journey to understanding AWS! 🌟

## ✔️ What is AWS?

**Amazon Web Services (AWS)** is a leading cloud service provider that offers a vast array of cloud computing services and resources. These services are hosted on a global network of data centres, enabling businesses and individuals to access and utilize computing power, storage, databases, networking, analytics, machine learning, and more over the public internet.

**Key Features and Advantages of AWS:**

1. **Infrastructure Management:** AWS takes care of the underlying hardware and infrastructure management, including servers, storage, and networking. This means users don't have to worry about physical hardware procurement, maintenance, or scaling.
    
2. **Elasticity and Scalability:** AWS provides the ability to scale resources up or down based on demand. This elasticity ensures that you can easily accommodate fluctuations in traffic, reducing costs during periods of lower demand.
    
3. **Regions and Availability Zones:** AWS operates in 25 geographic regions worldwide, with multiple Availability Zones within each region. These Availability Zones are isolated data centres with redundant power, networking, and cooling, designed to provide high availability and fault tolerance.
    
4. **Content Delivery Network (CDN):** AWS has a global network of over 200 edge locations as part of its Content Delivery Network (CDN). This network accelerates the delivery of content, like web pages and media, to end-users, improving performance and reducing latency.
    
5. **Pay-as-You-Go Model:** AWS follows a pay-as-you-go pricing model. Users are charged only for the resources they consume, making it cost-effective and eliminating the need for large upfront investments.
    

## ✔️ IAM service

**IAM (Identity and Access Management) in AWS** is a crucial service that allows you to manage access to your AWS resources securely. It ensures that users, whether they are individuals or services, have the appropriate permissions to perform actions on AWS resources while maintaining the principle of least privilege.

Here are the key concepts within IAM:

1. **User:**
    
    An IAM user represents a person or an entity that interacts with your AWS account. Users have their own set of credentials ( username and password) or access keys (programmatic access) to authenticate themselves to AWS services. IAM users are used to establish and manage individual identities within your AWS account.
    
2. **Groups:**
    
    Groups are a way to organize IAM users. Instead of assigning permissions to individual users, you can create groups and attach policies to these groups. Users added to a group inherit the permissions associated with that group.
    
    This simplifies permission management, especially in scenarios where multiple users require the same level of access.
    
3. **Policy:**
    
    A policy is a document that specifies the permissions and actions that are allowed or denied for users, groups, or roles. Policies are JSON documents that define the rules governing access to AWS resources.
    
    You can attach policies to users, groups, or roles to control what actions they can perform on AWS resources. Policies are essential for enforcing security and access controls in AWS.
    
4. **Role:**
    
    IAM roles are used to delegate permissions to AWS services or external entities securely. Unlike users and groups, roles are not associated with a specific identity or user account. Instead, roles are assumed by AWS services, EC2 instances, or even users from other AWS accounts through a process called role assumption.
    
    Roles are commonly used to grant temporary access to AWS resources or allow AWS services to interact with each other while maintaining security.
    

## ✔️ IAM hands-on practice

Now that we have discussed about the IAM service in AWS let's do some hands-on practice to solidify our knowledge.

### 🔸 Task 1: Creating IAM user and attaching policies

Here are the steps to follow for creating an IAM user and attaching policies:

1. Search for IAM and add it to your favorites so that you can access it easily from the navigation bar. Next, navigate to the IAM dashboard by clicking on the IAM service.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695953674590/965ee34d-971b-49ad-9ae2-8b91493a3668.png align="center")
    
2. In the IAM dashboard, click on the *Users* link in the sidebar or the main section. Next, click on `Create User` button on the right side of the screen.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695953838152/cffca0f1-7c73-4262-8acd-87fd15c3931d.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695953927204/8af36392-9ce0-41a8-9a46-f42fe1b1bd32.png align="center")
    
3. For Step 1 in creating a user (Specifying user details), first provide the user's name. Next, choose the *I want to create an IAM user* option. Then, select the *Autogenerated Password* option in the Console password section. Afterwards, choose the *Users must create a new password at the next sign-in* option. Finally, click on `Next`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695954062850/36c35ca1-7322-476e-bd59-3d45faec4c1b.png align="center")
    
4. For Step 2 in creating a user (Setting Permissions), select Attach Policy Directly under the Permissions Options. Then, in the search bar, search for S3 and choose the *AmazonS3FullAccess* option. This will grant the IAM user the ability to create, view, edit, and delete S3 resources within the AWS account. Finally, click on `Next`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695954467204/507d43a4-39fe-4667-8c34-b70954bb0390.png align="center")
    
5. For step 3 in creating a user (Review and Create), review the selected options and click on `Create User`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695954702812/d328ca67-9186-443a-b07b-31afc5b49575.png align="center")
    
6. After the user is created we will be given the password, and we can log in to the AWS console using the given credentials. Click on `Download .csv file` to save it in an excel file.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695954814329/9606ec52-9b10-47c8-bfe0-ff71a73a3717.png align="center")
    
7. To test the newly created user, log out of your AWS account and navigate to the .csv file you just downloaded. Copy the Console sign-in URL and paste it into your browser. Next, enter the IAM username and password, and click on `Sign In`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695955303124/4def2b81-d13e-4f08-9617-5095c2170c00.png align="center")
    
8. Now, you will be prompted to change the password. Enter the current and new passwords, and then click on `Confirm Password Change`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695955483118/5dc7bea2-8769-4c6a-951a-1a99acb9a546.png align="center")
    
9. Now, you will be logged in as the IAM user you just created.
    

Let's test the permissions that we applied to the IAM user.

1. Search for the s3 resource and go to it's dashboard.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695955754501/a8476471-86b2-4172-bd0b-37926e340ffe.png align="center")
    
    You will see the following screen since you have not created any buckets. Now, click on `Create Bucket`.
    
2. Simply provide the name of the bucket (since S3 buckets are globally unique, choose a very specific name to avoid naming errors) and don't worry about the other options. Just scroll to the bottom and click on `Create Bucket`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695955939862/756707ea-f533-4ab7-a56f-e0dc06c25c74.png align="center")
    
3. Now that your S3 bucket is created, you can edit it, view its contents, and delete it as necessary. These actions are allowed because the IAM user has full access to the S3 resource.
    
4. Now, let's attempt to create an EC2 instance (this is simply a virtual machine managed by AWS).
    
5. Navigate to the search bar and search for EC2, then proceed to its dashboard. You will encounter a bunch of errors. This occurs because our IAM user has access only to the S3 bucket resource and nothing else.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695956278918/4b096fa1-c2c9-454f-8852-a284d431f6ad.png align="center")
    

### 🔸 Task 2: Creating Groups and adding users

When you have multiple employees in an organization, they will each have their own IAM account. However, changing permissions for them individually can become very hectic. To tackle this problem, we can use the concept of Groups in AWS.

By creating a group, attaching policies to it, and adding users to the group, the users will then inherit the properties that have been applied to the group.

Let's see how can we create a group and add users to it. Sign in as the root user to perform the following steps.

1. In the IAM dashboard go to the Groups section and click on `Create Group`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695958210395/6bce5666-9b25-462a-b804-ca103117f2e8.png align="center")
    
2. Assign a name to the group and include the test-iam-user within the group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695958249056/d5af7a31-20c0-466a-a1e4-d01a2a4b078d.png align="center")
    
3. For the permissions search "ec2fullaccess" and select the *AmazonEC2FullAccess* permission, search for "s3readonly" and now select the *AmazonS3ReadOnlyAccess* permission.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695958309815/68eabaf9-3d70-4080-ae14-2e89cce78824.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695958293064/8e71eb09-793f-4eb7-bfd4-b89c81b950ed.png align="center")
    
4. Finally, click on `Create a Group`
    

Now our group is created, but wait the test-iam-user has full access of the s3 resource but in our group, we have specified read-only access for the s3 resource, how will that work out, let's see with an example.

Sign in as the test-iam-user in the AWS console.

1. Go to the s3 dashboard and try to create a new bucket, you will see that you can create or delete a s3 bucket even when in the group we have specified the users to have read-only access to the s3 resource.
    
    Let's log in to the AWS console as admin and see what's happening. Select the test-iam-user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695958032041/3b88c976-5531-4392-a205-7e29abf56875.png align="center")
    
    We can see that two policies are attached by the group and two that we attached directly. So we can conclude that the permissions that are attached directly to the user override the permission applied by the group.
    
2. Now to the ec2 dashboard, you will not see the errors. This is because the group has full ec2 access and the test-iam-user has inherited those permissions.
    

## 📍 Conclusion

In conclusion, as a DevOps engineer, it is essential to limit user access according to their specific needs to prevent potential damage to the production environment. The IAM service is a very powerful tool for restricting user access, and I encourage you to practice it as much as possible to become proficient in its use.

I am thrilled that you've learned something new today! Please, share your thoughts about what you loved in today's blog, and if you have any questions or doubts, don't hesitate to mention them in the comments! Let's keep the excitement going!