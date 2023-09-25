---
title: "🏗️ Terraform cloud providers:  provisioning infrastructure on cloud ☁️"
seoTitle: "🏗️ Terraform cloud providers:  provisioning infrastructure on cloud ☁"
datePublished: Mon Sep 25 2023 14:45:28 GMT+0000 (Coordinated Universal Time)
cuid: clmz03bde000j09mk3ngvcjw3
slug: terraform-cloud-providers-provisioning-infrastructure-on-cloud
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695609040626/433060c5-790e-4db7-8d71-b269c4315078.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695609061780/4f9b2af5-866d-47c8-94bb-ce9c0a8cf3c6.png
tags: devops, terraform, 90daysofdevops, trainwithshubham, terraweekchallenge

---

## 📍 Introduction

In today's blog, we're diving into the concept of terraform providers! 🎉 These incredible plugins, brought to you by Terraform, empower us to create mind-blowing infrastructure resources on cloud platforms like AWS, GCP, and Azure! Let's get started! 🚀

## ✔️What are terraform providers?

Terraform providers are plugins that enable Terraform to interact with various cloud platforms, infrastructure services, and APIs. Providers are responsible for understanding API interactions and exposing resources that can be managed using Terraform. Some popular providers include AWS, Azure, Google Cloud, and others.

Terraform providers are crucial components of the Terraform ecosystem as they enable interaction with various infrastructure platforms and services

Benefits of using terraform providers:

* Cross-Platform Compatibility
    
* Declarative Configuration
    
* Infrastructure as Code (IaC)
    

To use a provider, you need to declare it in your Terraform configuration file (which is usually a `terraform.tf` file). Here's an example of the AWS provider:

```yaml
provider "aws" {
  region = "ap-south-1"
}
```

## ✔️ Configuring and authenticating provider

When using aws provider for terraform we can use the AWS CLI to login to our aws account using an IAM user or we can use the credentials of an IAM user to specify in the provider configuration (this is usually not allowed as the credentials are exposed)

Authentication mechanisms in Terraform vary depending on the provider you are using. Here are a few common authentication methods:

1. `Access Key and Secret Key:` Many providers, such as AWS, utilize access keys and secret keys for authentication. You can acquire these keys from your cloud provider's management console.
    
2. `API Tokens:` Some services, like DigitalOcean or GitHub, use API tokens to check who you are. These tokens are made by the service and can be set up in the provider section.
    
3. `Service Principals:` Providers like Azure and Google Cloud usually use service principals to check who you are. A service principal is an ID with certain roles and rights in the cloud platform. To prove who you are with these providers, you usually set up important details like client ID, client secret, subscription ID, and so on.
    
4. `Environment Variables:` Terraform also supports authentication via environment variables. Instead of specifying credentials directly in the provider block, you can set environment variables with the required values, and Terraform will use them automatically. The naming conventions for these variables vary depending on the provider. For example, `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` is used for AWS.
    

```yaml
provider "aws" {
  region     = "ap-south-1"
  access_key = "your_access_key"
  secret_key = "your_secret_key"
}
```

## ✔️ Provisioning infrastructure on AWS using terraform

Let's provision ec2 instance on AWS using terraform.

Save the following file as `main.tf` in a directory.

```yaml
# creating key pair to ssh into the instance
resource "aws_key_pair" "mykey" {
  key_name   = "id_rsa"
  public_key = file("/home/ubuntu/.ssh/id_rsa.pub")
}
# declaring the default VPC
resource "aws_default_vpc" "default_vpc" {}
# creating a security group to attach to the instance
resource "aws_security_group" "allow_ssh" {

  name = "allow_ssh"
  tags = {
    Name = "allow_ssh"
  }
  # using default vpc
  vpc_id = aws_default_vpc.default_vpc.id
  ingress {
    description = "ssh access to ec2 instances"

    # inbound and outbound rules
    from_port = 22
    to_port   = 22
    protocol  = "tcp"

    # allows all traffic
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# creating an ec2 instance
resource "aws_instance" "myec2instance" {
count = 2
  ami             = var.ami_id
  instance_type   = var.instance_type
  key_name        = aws_key_pair.mykey.key_name
  security_groups = [aws_security_group.allow_ssh.name]
  tags = {
    Name = "terraform-instance"
  }
}
```

After creating the necessary terraform files, follow the below instructions

1. `terraform init` - Initialize the Terraform working directory. This command downloads the required provider plugins and establishes the backend for storing the Terraform state.
    

1. `terraform plan` - This command creates an execution plan.
    

1. `terraform apply` - This command applies all changes to the infrastructure.
    

## 📍 Conclusion

🎉 Thanks for reading my blog! I truly hope it was super informative for you! If you loved the content, please smash that like button, share it with everyone you know, and follow me for more amazing posts like this in the future! 🚀🌟