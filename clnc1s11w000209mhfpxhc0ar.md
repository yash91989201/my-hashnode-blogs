---
title: "⚙️ Setting up an Application Load Balancer with AWS EC2  ⚖️ ☁"
seoTitle: "⚙️ Setting up an Application Load Balancer with AWS EC2  ⚖️ ☁"
datePublished: Wed Oct 04 2023 17:53:41 GMT+0000 (Coordinated Universal Time)
cuid: clnc1s11w000209mhfpxhc0ar
slug: setting-up-an-application-load-balancer-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695611278199/530beb98-b516-4eea-a96b-af203471a66d.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695611302871/37ce34be-96c3-447c-a84a-8a333e4d54af.png
tags: aws, devops, load-balancer, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

Hey readers! Today in the [AWS Cloud DevOps ☁ series](https://yashraj-jaiswal.hashnode.dev/series/aws-cloud-devops), we will be exploring load balancers and target groups. For the hands-on practice, we will be creating load balancers and using them with auto-scaling groups.

## ✔️What is an AWS elastic load balancer?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696430400508/5937f0bc-612e-47f0-b22d-f70c8462e809.png align="center")

AWS Elastic Load Balancing (ELB) automatically distributes incoming application traffic across multiple targets, such as containers, EC2 instances, and IP addresses in one or more availability zones.

This process balances the distribution of frontend traffic to backend servers, enhancing the fault tolerance and availability of user applications. AWS load balancing also monitors the health of registered targets and routes traffic accordingly.

### ✔️ Working of AWS elastic load balancer

The AWS load balancer increases application availability by serving as a single point of contact for clients. Users can seamlessly add and remove instances from the AWS load balancer without disrupting the overall request flow to the application as needs change over time. In this way, AWS elastic load balancing scales as application traffic fluctuates and can in fact scale to most workloads automatically.

Users can add one or more listeners to the load balancer. A listener utilizes the specified port and protocol to monitor connection requests from clients and forwards these requests using the designated port number and protocol to registered instances. Health checks guarantee that the AWS load balancer directs requests exclusively to healthy instances.

The AWS load balancer, by default, evenly distributes traffic across enabled availability zones. To enhance fault tolerance, ensure that instances are maintained in roughly equal numbers across availability zones. Additionally, you can enable cross-zone load balancing, which supports uniform traffic distribution across all registered instances in this type of elastic load balancing.

## ✔️ Types of elastic load balancers

1. `application load balancer:`
    
    AWS Elastic Load Balancing evenly spreads incoming traffic to various targets like EC2 instances, containers, and IP addresses in different Availability Zones. The Application Load Balancer is a flexible option that works at the application level and offers advanced routing and content-based traffic control.
    
2. `network load balancer:`
    
    AWS Elastic Load Balancing evenly distributes incoming traffic to various targets like EC2 instances, containers, and IP addresses in different zones. The Network Load Balancer is a high-performance option that works at the transport layer (Layer 4) of the OSI model.
    
3. `gateway load balancer:`
    
    AWS Elastic Load Balancing easily spreads incoming network traffic among different targets like EC2 instances, containers, and IP addresses, while checking their health. The Gateway Load Balancer is a special option made for setting up and handling virtual appliances.
    
4. `classic load balancer:`
    
    Classic Load Balancer (CLB) is a legacy load balancer that is no longer recommended for new applications. It is a Layer 4 load balancer that operates at the TCP/IP level and distributes traffic based on source IP address, port number, and protocol. CLB supports both HTTP and TCP applications.
    

## ✔️ Load balancer hands-on practice

### 🔸 Task 1: Setup ec2 instances with load balancing

In our [previous blog post](https://yashraj-jaiswal.hashnode.dev/aws-elastic-compute-cloud-ec2-and-automating-ec2-processes), we created a launch template and auto-scaling group, we can just update the launch template to use it for this task.

Follow these steps to edit or create a new version of your launch template.

1. Go to the launch template section and select the created launch template.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696437161188/bf84621e-b506-428c-af4e-d2f73240054f.png align="center")
    
2. Open the Action dropdown and select `Modify template (Create new version)` option.
    
3. Go to the bottom of the screen and in the User details section within the Advanced details section paste the following script.
    
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
    
    echo "<html><body><h1>This html page is serve by ec2 instance with hostname:  $(hostname)</h1></body></html>" > /var/www/html/index.html
    
    # Restart Apache to apply changes
    sudo systemctl restart apache2
    ```
    
4. After pasting the above bash script click on Create template version.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696437419865/62ffcf79-b699-4082-a403-0573e944ef6f.png align="center")
    
5. Now that we have updated our launch template we can use this to create two instances.
    

Now we will create a load balancer and attach two ec2 instances to it using the target group.

1. Using the updated launch template create two new ec2 instances.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438613608/94205ea6-f67b-44c0-8140-71bdd8ab90bb.png align="center")
    
2. Go to the target group section and create a new target group.
    
3. Keep all the settings a default just give a name for your target group. Go to the bottom and click on next.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438691379/7f1291a9-481a-490e-81a5-8698aa462dc5.png align="center")
    
4. Select the newly created instances as a target and click on Include as pending below.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438744936/709cdae9-6884-44ab-bff8-5acd01438215.png align="center")
    
5. And then click on Create Target Group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438812517/97726bb4-c1ae-4002-be48-0c7a442f1bc8.png align="center")
    
6. Now go to the load balancer section and click on Create load balancer.
    
7. Click on Create in the application load balancer.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438873608/ff2334cc-3cfb-499a-8660-9014998411cb.png align="center")
    
8. Give a name for your load balancer.
    
9. Keep the other settings intact and for the network settings select two subnets.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438949066/982e0430-c11e-4554-8015-86bf1476344e.png align="center")
    
10. For the Listeners and routing section, select the newly created target group.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438982941/f5cd4557-d667-4614-a6d1-beae756d3fec.png align="center")
    
11. Go to the bottom and click on Create Load balancer.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696439009585/f20b0214-0fe8-42b0-b855-9e184c52de88.png align="center")
    
12. It will take some time to provision the load balancer and after some time in the dashboard, you will see that the load balancer is active.
    
13. Copy the DNS name of the load balancer and paste it into the browser.
    
14. Now, continue refreshing the browser tab, and you will notice that the HTML page is being served from different EC2 instances, as indicated by the changing hostname.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696439974820/07bd6a21-468b-431c-93ad-a231bfe6f08c.gif align="center")
    

### 🔸 Task 2: Setup aws load balancer with auto-scaling group

Now that we have created a load balancer and target group we can also apply auto-scaling which will increase the number of ec2 instances as per the traffic on the ec2 instances.

Refer to [this blog](https://yashraj-jaiswal.hashnode.dev/aws-elastic-compute-cloud-ec2-and-automating-ec2-processes#heading-task-2-creating-an-auto-scaling-group) to learn how to create an auto-scaling group. Now change the below settings to attach the load balancer to the auto scaling group. Rest of the steps will remain the same.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696440274020/2fc36ff9-feb0-409b-a0be-c0c4cad15a0b.png align="center")

After that go to the ec2 dashboard and you will see two additional ec2 instances are created other than the ones created from before.

## 📍 Conclusion

In this article, we explored AWS Elastic Load Balancer and its types, including the Application Load Balancer. We demonstrated how to set up a load balancer with EC2 instances and integrate it with an auto-scaling group. By implementing these concepts, you can ensure high availability and fault tolerance for your applications, efficiently managing traffic and scaling your resources as needed.

In the next blog of our [AWS Cloud DevOps ☁](https://yashraj-jaiswal.hashnode.dev/series/aws-cloud-devops) series, we will learn how to use the Command Line Interface to access AWS resources like S3 and ec2 instances.