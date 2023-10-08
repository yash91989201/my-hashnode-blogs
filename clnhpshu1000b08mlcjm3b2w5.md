---
title: "💾 Managed Relational Database service in AWS ☁"
seoTitle: "💾 Managed Relational Database service in AWS ☁"
datePublished: Sun Oct 08 2023 17:04:44 GMT+0000 (Coordinated Universal Time)
cuid: clnhpshu1000b08mlcjm3b2w5
slug: managed-relational-database-service-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696520151434/ed95d1c6-cd9a-4e4b-b2cd-d162023b6402.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1696520213121/bc934323-d19d-484d-a04a-f093843bb75e.png
tags: devops, aws-rds, 90daysofdevops, trainwithshubham, aws-rds-instance

---

## 📍 Introduction

Hello learners! Today, we will explore another managed offering from AWS: RDS. RDS is a managed database service provided by AWS, supporting various engines such as Aurora, MySQL, PostgreSQL, and many more. We will delve into the details of relational databases, discuss the features of RDS, and also engage in hands-on practice related to RDS.

Additionally, if you missed yesterday's blog post in which we explored accessing AWS resources like S3 using the command line, you can read it [here](https://yashraj-jaiswal.hashnode.dev/accessing-s3-resource-programmatically-using-the-aws-cli#heading-conclusion). Do take a look at the [AWS Cloud DevOps ☁](https://yashraj-jaiswal.hashnode.dev/series/aws-cloud-devops) series.

## ✔️ What is a relational database?

A relational database service offered by Amazon Web Services is called Amazon RDS. An example of a database type that stores data in tables with rows and columns is a relational database. An affordable, resizable relational database that meets industrial standards is offered by Amazon RDS. It offers customers ways to set up, run, and scale a relational database more easily in the cloud. Amazon RDS.

### 🔸 Features of RDS

* Oversees backups, recovery, automatic failure detection, and software patching.
    
* Offers a choice between manual backup snapshots and automated backups.
    
* Allows restoration of backups in case of data loss.
    
* Provides freedom to choose from MySQL, MariaDB, PostgreSQL, Oracle, and Microsoft SQL Server as database engines.
    
* Utilizes AWS IAM (Identity and Access Management) for enhanced security.
    

### 🔸**Amazon RDS Pricing**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696776749165/d2fe842c-832b-43cb-a7fa-981d85d6d586.png align="center")

You can test your environment using the basic settings of Amazon RDS for free. If you set up Amazon RDS for your business with more frequent usage, the costs will vary depending on how resources are utilized.

The cost of Amazon RDS depends on several different database engines, including Amazon Aurora, MySQL, PostgreSQL, MariaDB, Oracle, and Microsoft SQL Server.

The following parameters are used to determine the operating cost of Amazon RDS: Reserved Instances, On-Demand DB Instances, Backup Storage Snapshots, and Export Data Transfer.

## ✔️ RDS hands-on practice

### 🔸 Task 1: Creating RDS instance on AWS

Follow the given steps to create your own RDS instance on AWS.

1. Go to the RDS dashboard and click on `Create Database`
    
2. Keep `Standard Create` as selected for the `Database creation method`. And then select `PostgreSQL` as the engine type.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696781478838/735151b7-8053-4e28-bb27-94fa7a8c93b8.png align="center")
    
3. For the templates section select the free tier as we do not want to incur any cost.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696781541637/bacd282b-1c19-45e3-ae61-943bb21b0e6a.png align="center")
    
4. Set a username and password for the PostgreSQL database, and be sure to save these credentials, as you will need them later for logging in to the database.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696781645278/0acbf6e9-8689-47be-a7ad-24eaa39e5685.png align="center")
    
5. In the connectivity section, allow public access and modify the following settings: choose a security group that permits access to port 5432 (the port on which the PostgreSQL server responds), and select an available zone.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696781731574/db724f19-a61b-4c35-a1aa-d363f3345c4f.png align="center")
    
6. For the database authentication method, select password authentication.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696781910825/68df18eb-b202-443e-9528-aab6a05f09ae.png align="center")
    
7. Now in the Additional Configuration section enter an initial database name.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696781996326/17767553-9198-43f2-ac78-03779aa6d1a5.png align="center")
    
8. After applying all the settings scroll to the bottom and click on `Create Database.`
    
9. It will take around 10-15 min for the database to be up and running. And once it starts we can connect to it using the provided endpoint.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696782578851/63e64f6a-d500-4bcd-9199-0dd4b3241d4d.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696782628917/55fe03eb-8c7b-4e7e-ad4e-9a40d993e7fd.png align="center")
    

### 🔸 Task 2: Connecting to RDS instance and executing SQL commands

We can connect to the RDS instance using the endpoint that we got after the database was up and running.

To connect to your RDS instance, first create an ec2 instance then follow the below steps:

```bash
sudo su 
# 1. install postgresql
apt update && apt install postgresql -y 
# 2. connect to RDS instance using postgres credentials
# execute the following command and enter the admin password.
psql -h <RDS endpoint> -U <RDS admin user> 
```

After entering the password you will be logged into the RDS Postgres instance. Now change to the database that you provided as an initial database while creating the RDS instance, by entering the command like `\c database_name`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696783902267/18abddab-2d49-4b97-a129-f9522fcd1ab0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696784091051/e784d557-55ad-4a2f-a14a-691313a1264d.png align="center")

You can provide the endpoint in your application so that it can use the RDS instance as its data storage.

## 📍 Conclusion

In conclusion, Amazon RDS is a powerful, managed relational database service offered by AWS that simplifies the process of setting up, running, and scaling a relational database in the cloud.

Hey there! I hope you found this information helpful. If you did, please feel free to give this blog a like and share it with others who might find it useful too. If you want to learn more about DevOps and cloud, feel free to connect with me on [LinkedIn!](https://www.linkedin.com/in/yashraj-jaiswal-91989201s/) 😊