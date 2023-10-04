---
title: "👩‍💻 AWS Elastic Compute Cloud (EC2) and automating EC2 Processes 🔧"
seoTitle: "👩‍💻 AWS Elastic Compute Cloud (EC2) and automating EC2 Processes 🔧"
datePublished: Tue Oct 03 2023 17:11:35 GMT+0000 (Coordinated Universal Time)
cuid: clnaku1fn000109md5sfd08mx
slug: aws-elastic-compute-cloud-ec2-and-automating-ec2-processes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695610907600/4597e186-ab67-4551-b47c-61a7b7fdb378.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695610937677/5eabdc7b-e5e2-41d8-b9cc-71b5d55993ad.png
tags: ec2, aws, devops, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

Hey readers! Today in the [AWS Cloud DevOps ☁](https://yashraj-jaiswal.hashnode.dev/series/aws-cloud-devops) series, we will be exploring EC2 instances, launch templates, and auto-scaling groups. EC2 instances allow us to host our websites on managed Linux machines, while features like launch templates and auto-scaling groups enable us to scale our websites according to user demand.

## ✔️What is ec2 ?

Just like IAM, AWS provides a service called Elastic Compute Cloud (EC2) which is a virtual machine on the cloud. We can install different operating systems like Windows, Linux or Mac OS which is referred to as AMI (Amazon Machine Image). We can connect to an ec2 instance using SSH and configure it to serve our website as well.

Let's see how to launch an EC2 instance:

1. Go to the ec2 dashboard and click on `Launch Instance`
    
2. Give a name for your instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696347711781/c1a93ea6-060c-4bd5-90cf-2edb94f4c2e7.png align="center")
    
3. Select Ubuntu or any AMI for instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696347751409/c3a30ee2-f968-4e03-acae-60dcf91123b4.png align="center")
    
4. Create a new key pair if you don't have one already.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696347804773/fbdc36fe-b814-4343-a5ed-a18b23958257.png align="center")
    
5. Then click on the Launch Instance button on the right side.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696347895986/a92e87a8-a1bd-4626-9fb4-36b94528f090.png align="center")
    

Now your instance will be running in a minute and you can connect to it by selecting the instance on the ec2 dashboard and clicking on the connect button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696347950789/0cef7a75-b559-4b8a-9b31-23253e51bb37.png align="center")

## ✔️Launch template in ec2

A launch template is similar to a launch configuration, as it specifies instance configuration information. This includes the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and other parameters used to launch EC2 instances. However, using a launch template rather than a launch configuration enables you to maintain multiple versions of a launch template.

## ✔️ Auto Scaling group

When hosting your website on an EC2 instance, it is crucial to increase the number of instances when visitor traffic increases and decrease them when traffic subsides. This approach helps manage the load on the EC2 instances and ensures that visitors do not experience downtime or lag due to excessive server load.

To address this situation, we can utilize an auto-scaling group that allows us to specify the minimum number of instances to maintain at any given time, as well as the conditions under which the number of instances should increase, such as a rise in CPU utilization that may occur when the number of visitors to your website increases.

## ✔️ EC2 hands-on practice

### 🔸 Task 1: Creating an ec2 launch template

Follow the below-given steps to create a launch template:

1. Click on "Launch Template".
    
2. Enter a template name and, template tags.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696349973148/8f6b3be6-0942-421a-a17e-3060f749e5cf.png align="center")
    
3. Select AMI for instance preferrably ubuntu.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696350056664/a170cf97-3d73-483d-957f-c6c5e06834f9.png align="center")
    
4. Then select t2.micro as the instance type.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696350112833/b4569b28-268c-4349-a661-ee5efe30c13f.png align="center")
    
5. Select a key pair to connect to the instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696350173016/6443fb5b-25c2-429f-b67d-0b12c875ce18.png align="center")
    
6. Then paste the following script in User Data section within the advanced details section.
    
    ```bash
    #!/bin/bash
    
    # Update the package list
    sudo apt update
    
    # Install Apache
    sudo apt install -y apache2
    
    # Enable Apache to start on boot
    sudo systemctl enable apache2
    
    # Start the Apache service
    sudo systemctl start apache2
    
    # Clone the GitHub repository
    git clone https://github.com/yash91989201/simple-website.git
    
    # Copy the HTML file to the Apache web root directory
    sudo cp simple-website/index.html /var/www/html/
    
    
    # Restart Apache to apply changes
    sudo systemctl restart apache2
    
    # Clean up - remove the cloned repository
    rm -rf simple-website
    
    echo "Apache web server is installed and your HTML page is now being served."
    ```
    

You can now utilize this launch template to create multiple EC2 instances and configure auto-scaling groups as well.

To use a launch template to create an EC2 instance, follow the steps provided.

* Go to EC2 dashboard
    
* Click the dropdown icon beside the "Launch Instance" button
    
* Select the "Launch Instance from Template" option
    
* Enter the number of instances
    
* Click on "Launch Instance"
    
* Instances will be launched with Apache2 serving the simple website
    

### 🔸 Task 2: Creating an auto-scaling group

To create an auto-scaling group with the above-created launch template follow the below steps:

1. Select Auto-Scaling Group in the sidebar of ec2 dashboard.
    
2. Name your auto-scaling group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696350996460/07f14e1d-ff88-46f6-9bf9-9b151b59b4d4.png align="center")
    
3. Select the launch template that we created just now then click on the Next button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696351055255/fd48a194-6f4c-4580-acc1-57a1f5b8dea1.png align="center")
    
4. Select two subnets in the instance launch options then click on the Next button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696351102143/4d56330c-79b1-4d17-8804-b17ec580230d.png align="center")
    
5. Click on the next button for this step.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696351150880/bf7d1951-a488-4a2d-b100-9c2963afca93.png align="center")
    
6. Now configure the group size policy, for the minimum set 2 and for the maximum set 4 Now the auto scaling group will ensure that at least 2 ec2 instances are running all the time even if something happens to any instance new one will be created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696351528574/a5ca268c-081f-49e1-830d-4f1bfd21ffc8.png align="center")
    
7. For the scaling policy, we will set an average CPU utilization limit, this means when the CPU usage on any instance is more than 60% another instance will be launched.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696351519977/7cd2e081-0078-4149-8877-6fcc00ee99c1.png align="center")
    
8. For the notification section just click on the next button.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696351587580/25573abc-2911-4f06-9a99-ef8cde6de57c.png align="center")
    
9. Click on the next button and then create an autoscaling group.
    
10. Now go to the ec2 dashboard and you will see that 2 ec2 instances are created and they will be hosting a website.
    

You can access the website by pasting the IP address of the ec2 instance in your browser.

To test the auto-scaling group you can try to delete one of the created ec2 instances and after some time you will see that a new instance will be created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696352636560/ce352ca9-bd36-45e0-85b5-6030b1d53636.gif align="center")

## 📍 Conclusion

In this article, we explored AWS Elastic Compute Cloud (EC2) and learned how to automate EC2 processes using launch templates and auto-scaling groups. By understanding these concepts, you can efficiently manage your EC2 instances, ensuring your website remains responsive and available even under heavy traffic. Auto-scaling groups help maintain optimal instance numbers, improving the overall performance and reliability of your cloud infrastructure.

In the next article of this series, we will explore load balancers and discuss how to make our website accessible to users.

I hope that you have learnt something new today! I'd love to hear what you enjoyed most about this blog post. If you have any questions or concerns, feel free to share them in the comments. Let's keep the excitement going!