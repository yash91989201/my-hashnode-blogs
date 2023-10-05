---
title: "👨‍💻 AWS CLI and IAM programmatic access : A comprehensive guide ℹ️"
seoTitle: "👨‍💻 AWS CLI and IAM programmatic access : A comprehensive guide ℹ️"
datePublished: Thu Oct 05 2023 15:20:13 GMT+0000 (Coordinated Universal Time)
cuid: clndbqitu000909l671xse0a8
slug: aws-cli-and-iam-programmatic-access-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695611595250/2999f88b-5c59-466b-b24d-d58635da327f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695611629617/4d538ef3-fd15-4799-aebf-673b303f517d.png
tags: ec2, iam, aws-cli, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

Hello readers! In the [previous blog](https://yashraj-jaiswal.hashnode.dev/setting-up-an-application-load-balancer-with-aws-ec2) of our [AWS Cloud DevOps ☁ series](https://yashraj-jaiswal.hashnode.dev/series/aws-cloud-devops), we learned how to create an Application Load Balancer in AWS and attach it to an Auto Scaling group. Now, let's explore how to access or create resources in our AWS infrastructure programmatically using the AWS CLI. For the hands-on practice section, we will create an IAM user for CLI access.

## ✔️ AWS CLI

Up until now, we have been creating resources in our AWS account using the provided user interface. However, we can also use commands to provision infrastructure on AWS programmatically. To do this, we can utilize the AWS CLI tool, which we can install and then configure with IAM credentials. Once configured, we can execute commands to perform tasks as needed.

Additionally, we can write Bash scripts using the commands provided by the AWS CLI to simplify our tasks. However, tools like Terraform, CloudFormation, and Pulumi are available for this purpose. Typically, we use the AWS CLI for performing quick tasks, such as creating one or two resources, where writing an entire configuration file is not practical.

## ✔️ AWS CLI hands-on practice

Let's engage in some hands-on practice by creating a setup for CLI access to our AWS account.

### 🔸 Task 1: Creating IAM user for CLI access

After installing the AWS CLI, it is necessary to connect it to our account to perform any tasks. This can be done by creating an IAM user with CLI access.

Follow the steps below to create an IAM user for CLI access:

1. Go to the IAM dashboard and create a new IAM user.
    
2. Specify user details and click on Next.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696517586439/69ceb3d7-a1f3-4dfb-ae0c-2a14a02e22ed.png align="center")
    
3. For permissions, choose `Attach Permission Directly` option and select `AdministratorAccess` then click on `Next`. Keep in mind that while we are granting AdministratorAccess for practice purposes, in real-world situations, you should only grant the necessary permissions to an IAM user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696517629359/cf509250-05e9-4297-b8c4-0bf671669e93.png align="center")
    
4. After the user has been created select it and you will be taken to the newly created IAM user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696517915791/4943d634-b151-4b89-ac0b-46299de9a930.png align="center")
    
5. Now select `Create access key` then on the next page choose the CLI option. Then scroll to the bottom click on the check box and then click on the `Next` button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696517999441/9c14b6db-8ea0-43b7-a7c9-1a3c8728aa2a.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696518009330/8e809e71-522c-4d36-91e9-b912cca01882.png align="center")
    
    Now for the next section provide a description and Create access key.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696518114458/9e094e3b-a99b-4d70-8e05-1047cea378c6.png align="center")
    
6. On the next page, you will see the access key and secret access save them by downloading as a .csv file.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696518223093/d6438745-ea46-4826-93c2-1c3c0d558e93.png align="center")
    
7. Now we can use these credentials to make changes in our aws account from the terminal itself.
    

### 🔸 Task 2: Configure AWS CLI for programmatic access.

To use the AWS CLI, we must first set it up. Follow the steps below to set up the AWS CLI on your local machine.

1. Firstly, download the [AWS CLI v2 Windows installer](https://awscli.amazonaws.com/AWSCLIV2-2.0.30.msi)
    
2. Start the installation and just click `Next` to proceed with the installation.
    
3. Finally, execute the `aws --version` command to confirm if the installation is successful.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696518353450/1ec649f6-6554-431c-a5f6-d886ae3ee73d.png align="center")
    
4. Execute the command `aws configure` and provide the access keys that we acquired earlier. Then enter the default region and output format.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696518488808/37087b47-92b8-4133-918c-931dd82bd580.png align="center")
    
5. Now, we can execute commands to obtain information about our AWS resources and create them as well. Since we have granted admin permissions to our IAM user we can access any information about our AWS account.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696518596344/b3ecd112-5e50-4a13-8df4-351f09302db6.png align="center")
    

## 📍 Conclusion

In conclusion, this comprehensive guide has demonstrated how to set up AWS CLI and IAM programmatic access. By following the hands-on practice, you can now create an IAM user for CLI access and configure the AWS CLI on your local machine. This will enable you to manage your AWS resources programmatically, streamlining your tasks and increasing efficiency.

In our upcoming blog, get ready for an exhilarating adventure as we dive into AWS CLI commands! Not only that, but we'll also be creating s3 buckets and EC2 instances with just a few simple commands!

I hope you learned something new! Do share your favourite part of this blog post. If you have questions, share them in the comments.