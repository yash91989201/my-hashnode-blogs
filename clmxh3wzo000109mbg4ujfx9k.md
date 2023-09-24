---
title: "Terraform Modules Explained: How to Achieve reusability in Terraform"
seoTitle: "Terraform Modules Explained: How to Achieve reusability in Terraform"
datePublished: Sun Sep 24 2023 13:06:17 GMT+0000 (Coordinated Universal Time)
cuid: clmxh3wzo000109mbg4ujfx9k
slug: terraform-modules-explained-how-to-achieve-reusability-in-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695560708361/1b3fad19-876d-4925-9100-6d9111243b6a.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695560755956/3ad5f521-c09e-4f54-8cc9-6c12559f3389.png
tags: devops, terraform, 90daysofdevops, trainwithshubham, terraweekchallenge

---

## Introduction

Up until now, we have been using multiple files for our Terraform configuration. Today, we will explore Terraform modules, which allow us to create reusable Terraform files that can be utilized at different stages of our software development process.

## What are modules in terraform?

Modules in Terraform enable us to create reusable infrastructure configurations that can be adapted for various purposes by supplying different variables.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695558207419/49f5fede-2034-4b44-9ca2-c322acf50a55.png align="center")

A Terraform module allows for the creation of a logical abstraction on top of a set of resources. In other words, a module lets you group resources and reuse this group later, potentially multiple times.

## Benefits of using modules in terraform

Modules are a fundamental idea in Terraform because they offer the following advantages:

1. **Code Reusability**: With modules, you can create a resource group once and use it in different projects or settings. This makes managing your infrastructure easier, promotes code sharing, and cuts down on repeated code.
    
2. **Abstraction**: With modules, you can change complex infrastructure parts into easy-to-use interfaces. This makes it simpler for teams to use Terraform without knowing all the details.
    
3. **Separation of Concerns**: Your infrastructure code can be split into smaller, easier-to-handle modules. Each module can focus on a specific part of your infrastructure (like networking, databases, or apps) and include the needed resources and adjustments.
    
4. **Collaboration**: Modules make it easier to create and manage different parts of your infrastructure, helping teams work together. Team members can work on separate modules to build the whole infrastructure.
    
5. **Testing**: Before adding them to the whole system, you can easily check if a module works because it can be tested on its own. This helps find mistakes and issues early in the development process.
    
6. **Versioning**: You can keep track of changes and updates to the module with versioning. This makes everything more consistent and helps manage changes in the infrastructure.
    
7. **Scalability**: Modules can make it simpler for you to scale your setups as your infrastructure expands. The same module can be used to produce many instances of the same resource type with various input variables.
    
8. **Documentation**: Clear documentation that comes with well-designed modules makes it simpler for users to grasp how to use them and what inputs they need.
    

## Creating a module

After gaining a solid understanding of modules, let's dive into creating our own Terraform module named demo-app.

This module will provision infrastructure components such as EC2 instances, S3, and DynamoDB for various software development lifecycle stages, including development, staging, and production.

When creating a module, we need to follow a specific folder structure. All the modules go within a folder named `modules`. So create a modules folder and within it create a folder named `demo-app`. Now you are ready to create a module in the `demo-app` folder.

### Step 1: Creating variable file for module

When creating a module, it is necessary to define variables for all the attributes in various resources as empty. This allows us to supply values when utilizing the module in different contexts.

```yaml
variable "ami_id" {
  description = "AMI id for ec2 instances"
  type        = string
}

variable "instance_type" {
  type        = string
  description = "instance type"
}

variable "instance_name" {
  type        = string
  description = "instance name"
}

variable "bucket_name" {
  type        = string
  description = "s3 bucket name"
}

variable "dynamodb_table_name" {
  type        = string
  description = "dynamo db table name"
}

variable "env_name" {
  type = string
  description = "different environments"
}
```

### Step 2: Creating terraform resources for different resources.

In this section, we will create various resources within separate files for each resource type. We will utilize variables to assign dynamic values to our resources.

1. ec2 terraform file:
    
    ```yaml
    # creating key pair to ssh into the instance
    resource "aws_key_pair" "mykey" {
      key_name   = "${var.env_name}_id_rsa"
      public_key = file("/home/ubuntu/.ssh/id_rsa.pub")
    }
    # declaring the default VPC
    resource "aws_default_vpc" "default_vpc" {}
    # creating a security group to attach to the instance
    resource "aws_security_group" "allow_ssh" {
    
      name = "${var.env_name}_allow_ssh"
      tags = {
        Name = "${var.env_name}_allow_ssh"
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
        Name = "${var.env_name}-${var.instance_name}"
      }
    }
    ```
    
2. s3 terraform file:
    
    ```yaml
    resource "aws_s3_bucket" "my_demo_bucket"{
    bucket = "${var.env_name}-${var.bucket_name}"
    }
    ```
    
3. dynamo\_db terraform file:
    
    ```yaml
    resource "aws_dynamodb_table" "my_demo_table" {
    
      name              = "${var.env_name}-${var.dynamodb_table_name}"
      billing_mode      = "PAY_PER_REQUEST"
      hash_key          = "emailID"
      attribute {
        name = "emailID"
        type = "S"
      }
    }
    ```
    

After we have created a module we must execute terraform init so that our module is registered in terraform.

### Step 3 : Using the module in main file

After we have created and registered the module we can use it in our main terraform file.

Here we have utilized module to provision infrastructure for dev, qa and prod phase.

```yaml
# dev infra
module "dev_demo_app" {
  source              = "./modules/demo-app"
  env_name            = "dev"
  instance_type       = "t2.micro"
  ami_id              = "ami-053b0d53c279acc90"
  instance_name       = "demo-instance"
  bucket_name         = "demo-s3-bucket"
  dynamodb_table_name = "batch4_"
}

# staging qa infra
module "qa_demo_app" {
  source              = "./modules/demo-app"
  env_name            = "qa"
  instance_type       = "t2.small"
  ami_id              = "ami-03a6eaae9938c858c"
  instance_name       = "demo-instance"
  bucket_name         = "demo-s3-bucket"
  dynamodb_table_name = "demo-table"
}

# prod infra
module "prod_demo_app" {
  source              = "./modules/demo-app"
  env_name            = "prod"
  instance_type       = "t2.large"
  ami_id              = "ami-026ebd4cfe2c043b2"
  instance_name       = "demo-instance"
  bucket_name         = "demo-s3-bucket"
  dynamodb_table_name = "demo-table"
}
```

### Step 4: Provisioning infrastructure using module.

Now that we have created modules we can use them to create all stages at once or create one stage at a time.

1. provisioning all at once: To provision all modules we can just execute the following command `terraform apply`
    
2. provision single module: We can also provide the target flag to specify which module to execute `terraform apply -target=module.prod-demo-app`
    

## Conclusion

In conclusion, Terraform modules provide a powerful way to achieve code reusability, abstraction, and separation of concerns for managing infrastructure. Taking advantage of modules helps simplify infrastructure management and promotes consistency across different stages of the software development lifecycle.