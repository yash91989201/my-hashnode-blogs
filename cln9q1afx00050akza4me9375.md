---
title: "🔍 Exploring IAM (Identity Access Management) in AWS: A comprehensive guide 📘"
seoTitle: "🔍 Exploring IAM  in AWS: A comprehensive guide 📘"
datePublished: Tue Oct 03 2023 02:49:25 GMT+0000 (Coordinated Universal Time)
cuid: cln9q1afx00050akza4me9375
slug: exploring-iam-identity-access-management-in-aws-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695610477038/1d39e150-7835-45cb-a3dd-5e931b567614.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695610538182/2a3b66d4-7549-4c0a-ab5b-e0ae81e1eba2.png
tags: aws, devops, iam, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

Hey readers! Today in the [AWS Cloud DevOps ☁](https://yashraj-jaiswal.hashnode.dev/series/aws-cloud-devops) series, we will be creating ec2 instances by providing a bash script that can install the required software beforehand.

## ✔️ AWS User Data

User Data in Amazon EC2 is a potent feature that enables you to automate the configuration of your instances upon launch. This functionality offers a convenient method for performing routine setup tasks, installing software, and executing scripts, thereby streamlining the process of getting your instances operational with the desired configurations.

By providing either shell scripts or cloud-init directives, you can tailor your instances to meet particular needs. This automation can save considerable time and effort, particularly when deploying multiple instances with similar configurations.

## ✔️ IAM hands-on practice

### 🔸 Task 1: Launch ec2 instance with jenkins already installed

Follow the given steps to install jenkins on an ec2 instance using User Data.

1. Go to the EC2 dashboard and click on Launch Instances and
    
2. Fill in details like instance name, type , AMI, security group, and key pair as per your requirement.
    
3. Scroll to the bottom and click on "Advanced Details" and then again scroll to the bottom.
    
4. Then in the User details section to add jenkins install script.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696300514653/eb2435be-29a7-4c68-af45-fdf4643e0dd9.avif align="center")
    
5. Launch the instance.
    
6. Update the security group to access jenkins.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696300530994/b29ebd12-e6f2-4d94-a7e3-319cd820ddc2.avif align="center")
    
7. Verify installation
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696300545941/592c4b6c-174e-4029-b86e-fd6d93b20bf2.avif align="center")
    
    To verify if Java and Jenkins are installed correctly or not execute the following commands.
    
    ```yaml
    java --version
    jenkins --version
    ```
    

### 🔸 Task 2: Creating IAM roles

Create three Roles named: DevOps-User, Test-User, and Admin. These three roles would have the following permissions.

* `DevOps-User`: `AmazonEC2FullAccess`
    
* `Test-User`: `AmazonEC2ReadOnlyAccess`
    
* `Admin`: `AdministratorAccess`
    

Follow the given steps to create new roles with permissions:

1. Go to the IAM dashboard and select the roles link.
    
2. Then click on Create Role.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696300870608/b545238d-0000-4fd1-a3d6-f687d1191fd7.png align="center")
    
3. And then search for ec2 in the use case search bar.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696300888071/7c20340b-a27a-4d19-b47a-e654f1c08654.png align="center")
    
4. Select the first option, that allows for all access.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696300850240/2cf82073-025e-4fbc-84fb-f4a9e6dcec8c.png align="center")
    
5. Click on next.
    
6. In the next section, search for "ec2full" and then select the ec2 full access option and then click on next.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696300984217/cd4d89ac-bc15-4932-b1eb-98aa56c87a2d.png align="center")
    
7. Enter the name of your role and click on "Create Role".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696301045403/a66f97b9-3255-4238-93c3-24f421ee982d.png align="center")
    
8. Now you the DevOps-User role has been created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696301109234/b8e0c3de-14e0-4612-835d-210bf386ecc0.png align="center")
    

## 📍 Conclusion

User Data is extremely useful for configuring your EC2 instances during their creation, opening up numerous automation possibilities when incorporating EC2 into your workflow.

Roles in IAM are very helpful if we want to apply certain permissions to a service in AWS.

I'm so glad you picked up some new knowledge today! I'd love to hear what you enjoyed most about this blog post. If you have any questions or concerns, feel free to share them in the comments. Let's keep the excitement going!

Let's connect on Linked In: [https://www.linkedin.com/in/yashraj-jaiswal-91989201s/](https://www.linkedin.com/in/yashraj-jaiswal-91989201s/)