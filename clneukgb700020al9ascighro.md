---
title: "🔐 Accessing S3 resource programmatically using the AWS CLI  👨‍💻 📁"
seoTitle: "🔐 Accessing S3 resource programmatically using the AWS CLI  👨‍💻 📁"
datePublished: Fri Oct 06 2023 16:55:08 GMT+0000 (Coordinated Universal Time)
cuid: clneukgb700020al9ascighro
slug: accessing-s3-resource-programmatically-using-the-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695611988097/fbe735b5-3202-4319-8689-bddb6e9adf06.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695612001773/c62868d1-368d-4094-bbab-099a37dbbade.png
tags: devops, aws-cli, 90daysofdevops, trainwithshubham, s3-bucket

---

## 📍 Introduction

Hello readers! In the [previous blog post](https://yashraj-jaiswal.hashnode.dev/aws-cli-and-iam-programmatic-access-a-comprehensive-guide) of our [AWS Cloud DevOps ☁](https://yashraj-jaiswal.hashnode.dev/aws-cli-and-iam-programmatic-access-a-comprehensive-guide) series, we learned about AWS CLI access and set it up using IAM credentials. Now, let's explore how we can use AWS CLI access to interact with resources in our account.

## ✔️ S3

Amazon Simple Storage Service (Amazon S3) is an object storage service offering industry-leading scalability, data availability, security, and performance. It caters to users of all sizes and industries, allowing them to store and protect any amount of data for various use cases. These include data lakes, websites, mobile applications, backup and restoration, archiving, enterprise applications, IoT devices, and big data analytics.

S3 offers management features that enable you to optimize, arrange, and configure data access to fulfil your unique business, organizational, and compliance needs.

### 🔸 Creating a S3 bucket

Creating a s3 bucket is fairly simple, follow the below steps to create a s3 bucket.

1. Go to the s3 dashboard and click on `Create a bucket`
    
2. Give a name for your bucket, do keep in mind that every bucket name must be globally unique.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608694503/bff87007-3ba6-44d2-9839-e5fbd752420b.png align="center")
    
3. By default, all public access to an S3 bucket is disabled, and the contents of the S3 bucket are accessed and served by AWS managed CDN called CloudFront.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608795372/56e07516-a1c2-4dd2-bff2-27d300055b69.png align="center")
    
4. Optionally, you can also enable bucket versioning. This means that every object updated in the S3 bucket will be tagged with a version name, allowing you to revert to that version if necessary.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696608932419/d8bde11b-3e51-4367-b358-7688c4f83122.png align="center")
    
    And then scroll to the bottom and click on `Create bucket`
    
5. Now that your S3 bucket has been created, you can go to the dashboard, select the S3 bucket you just created, and add objects to it. This can also be done programmatically.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696609031855/3ed56e29-b8b5-4719-a869-24708fee32f8.png align="center")
    

## ✔️ AWS CLI with S3 hands-on practice

To perform these tasks, you must have the AWS CLI installed on your system and configured with an IAM user with appropriate access. To accomplish this, you can refer to my [previous blog post](https://yashraj-jaiswal.hashnode.dev/aws-cli-and-iam-programmatic-access-a-comprehensive-guide#heading-aws-cli-hands-on-practice) where I explain how to do so.

Here is the list of AWS S3 command that you can use:

```bash
# list all s3 buckets in your account
aws s3 ls
# create a new s3 bucket with unique name
aws s3 mb s3://bucket-name 
# remove an existing bucket
aws s3 rb s3://bucket-name 
# copy a file in your local machine into s3 bucket
aws s3 cp file.txt s3://bucket-name
# download a file from s3 bucket
aws s3 cp s3://bucket-name/file.txt .
# copy all the contents of a folder into s3 bucket
aws s3 sync local-folder s3://bucket-name 
# list all the objects in a s3 bucket 
aws s3 ls s3://bucket-name 
# remote a single object from s3 bucket
aws s3 rm s3://bucket-name/file.txt
```

### 🔸 Task 1: Creating and deleting the s3 bucket with AWS CLI

Using the AWS CLI, we can manage the contents of an S3 bucket, as well as create or delete it. Let's explore some of the commands that assist us in accomplishing these tasks.

1. Creating a s3 bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696610013061/8eb3a149-63ba-42bd-9ba2-548d96d36cb4.gif align="center")
    
2. Deleting s3 bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696610020216/3882aec9-a89c-49f5-a344-91009e2849ee.gif align="center")
    

### 🔸 Task 2: Copying files to s3 bucket with AWS CLI

1. Copying a file to a s3 bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696610759008/1a3fdec4-500a-4442-9f17-bd9ca5870eea.gif align="center")
    
2. Syncing files in a folder to a s3 bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696610766093/d2cbf836-182e-4a64-9b6d-e6ee1433f770.gif align="center")
    

## 📍 Conclusion

In today's blog, we learned how to programmatically share resources between a local machine and an S3 bucket. In the upcoming blog, we will explore RDS, a Managed Relational Database Service by AWS.

If you learnt something new today, please consider liking and sharing the blog.