---
title: "Exploring Cloud Watch alarms and SNS topics in AWS."
datePublished: Tue Oct 10 2023 16:16:48 GMT+0000 (Coordinated Universal Time)
cuid: clnkiyjle000708ieb2jp1ecl
slug: exploring-cloud-watch-alarms-and-sns-topics-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696954509049/fd44c648-0279-40c6-84ca-775068f2edb3.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1696954600768/6d93d746-7df9-42f6-a3e5-6344087b3721.png
tags: aws, aws-cloudwatch, 90daysofdevops, trainwithshubham, sns-in-aws

---

## 📍 Introduction

Hello readers! After completing an incredible [project on RDS](https://yashraj-jaiswal.hashnode.dev/deploying-wordpress-on-aws-with-rds-as-database), let's dive into CloudWatch alarms and SNS topics. For hands-on practice, we'll create a CloudWatch alarm that monitors our AWS bill and sends us an email if it exceeds $2.

## ✔️ What is Amazon Cloud Watch?

Amazon CloudWatch actively monitors your Amazon Web Services (AWS) resources and the applications running on AWS in real time. CloudWatch allows you to collect and track metrics, which are measurable variables for your resources and applications. The CloudWatch home page automatically displays metrics about every AWS service you use. You can additionally create custom dashboards to display metrics about your custom applications and display custom collections of metrics that you choose.

CloudWatch alarms can be utilized in situations where specific actions are required based on particular metrics. You can create alarms that monitor metrics and send notifications or automatically modify the resources being monitored when a threshold is surpassed. Additionally, you can use Lambda functions to execute actions according to the metrics.

For example, you can monitor the CPU usage and disk reads and writes of your Amazon EC2 instances and then use that data to determine whether you should launch additional instances to handle increased load. You can also use this data to stop under-used instances to save money. With CloudWatch, you gain system-wide visibility into resource utilization, application performance, and operational health.

## ✔️ What is AWS SNS?

Amazon Simple Notification Service (Amazon SNS) is a managed service that facilitates message delivery from publishers to subscribers, also known as producers and consumers. Publishers communicate asynchronously with subscribers by sending messages to a topic, which serves as a logical access point and communication channel.

Clients can subscribe to an SNS topic and receive published messages through a supported endpoint type, such as Amazon Kinesis Data Firehose, Amazon SQS, AWS Lambda, HTTP, email, mobile push notifications, and mobile text messages (SMS).

## ✔️ Hands-On project

For the hands-on project, we will be building this.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696954233599/4c631b6d-a246-476f-bd39-a1f933a5cc6b.png align="center")

### 🔸 Task 1: Create a cloud watch alarm to send you an email when your bill reaches above $2

Before starting first we need to change some settings in our AWS account. Go to Billing Dashboard &gt; Billing Preferences &gt; Check "Receive cloud watch billing alerts" in the Alert Preferences and Update it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696910182753/e0c62175-1bae-48a0-a1dd-b2da406e02c0.png align="center")

1. Go to the Cloud Watch dashboard and click on alerts on the left sidebar. Then click on `Create Alarm` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696909323362/6228b9a0-0c76-4c6a-aa78-238d6e899f8b.png align="center")
    
2. Now specify the metric that you want to monitor. For our practice, we need to monitor the cost so that we can send out alerts based on the usage.
    
    Select the Cost Explorer and then click on `Select Metric` . Then on the popup select Billing &gt; Total Estimated Charge.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696910291635/453d3ebc-9784-421a-877a-5c41f752a692.png align="center")
    
3. Now, set the billing threshold to $2 or any amount you are willing to spend on learning AWS. Choose "Greater/Equal" and then define the threshold value.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696910332793/a3c8da02-0950-4d92-bff8-04299bb23a85.png align="center")
    
4. Now we need to create an SNS topic that will send the notification to our email.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696910565953/a89a2cc9-18e4-436b-b2ec-cdc9017839cf.png align="center")
    
    Now click on `Create topic` . Then click on Next.
    
5. Now add the content for the email.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696910756352/d8093e37-bf1a-4528-9014-07964272ff51.png align="center")
    
6. Now, navigate to Gmail and subscribe to the notifications. You may need to check the spam folder for this email.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696910855753/dfbbf852-e91e-496a-a977-65efb3229778.png align="center")
    
    Your alarm has been successfully set up.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696910909672/88e96a78-975f-487a-9fdd-1c726a240c25.png align="center")
    

Now, you will receive notifications whenever your bill surpasses a specific amount, allowing you to promptly stop/delete any unnecessary services.

## 📍 Conclusion

In conclusion, Amazon CloudWatch and Simple Notification Service (SNS) are powerful AWS tools that allow you to monitor your resources and applications, set alarms based on specific metrics, and receive notifications when certain thresholds are met.

By creating a CloudWatch alarm and an SNS topic, you can effectively manage your AWS billing and ensure that you stay informed about your usage costs.

Hey there! I hope you found this information helpful. If you did, please feel free to give this blog a like and share it with others who might find it useful too. If you want to learn more about DevOps and cloud, feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/yashraj-jaiswal-91989201s/)! 😊