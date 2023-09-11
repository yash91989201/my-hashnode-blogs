---
title: "Understanding Terraform: A Thorough Introduction to the Basics"
seoTitle: "Introduction to terraform basics"
datePublished: Mon Sep 11 2023 16:37:06 GMT+0000 (Coordinated Universal Time)
cuid: clmf3wykm000a09l7hz5nabz8
slug: understanding-terraform-a-thorough-introduction-to-the-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694450100384/2d4b8ae4-fc86-4641-ace7-9042063b101d.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1694450213974/9b550a4f-0f05-4765-bbc1-b24fe84f3738.png
tags: devops, terraform, 90daysofdevops, trainwithshubham, terraweekchallenge

---

## 📍 Introduction

Hey there, tech enthusiasts! 🎉 Ever wondered how massive company infrastructures are built? Not manually, that's for sure! They use something called "Infrastructure as Code"! 🤯 Today, we're diving into the world of Terraform, an incredible tool for provisioning infrastructure using code! 🚀

## ✔️ What is terraform?

Terraform can be defined as a tool for building and changing technical infrastructure. When using Terraform we use configuration files where we specify what element we want to create. Terraform is capable of determining what will change and building execution plans that can be used as configuration modifications.

We write our infrastructure configuration in a file with the extension `.tf` with the help of HCL (Hashicorp Configuration Language). Terraform allows us to work with different cloud providers like AWS, Azure and Google Cloud Platform.

## ✔️ 3 steps of using terraform

There are 3 steps that we need to follow to provision our infrastructure.

1. `terraform init:` This is just like git init, where we initialize Terraform in our directory and it keeps track of the different resources that we create through our configuration file.
    
2. `terraform plan:` Using the terraform plan command we can list all the changes that will be performed when we apply our configuration file.
    
3. `terraform apply:` This command applies all the changes specified in our configuration file.
    

## ✔️ Benefits of using terraform

1. **Improved collaboration:** It allows teams to define and manage infrastructure using version control, which makes it easier for multiple people to collaborate and work on the same codebase. This can help improve collaboration and reduce the risk of errors.
    
2. **Version history:** It automatically maintains a version history of your infrastructure, which makes it easy to roll back to previous versions if necessary. This can help protect against mistakes and ensure that you can recover from failures quickly.
    
3. **Consistency:** It allows you to define your infrastructure using a high-level configuration language, which means that you can specify the desired state of your infrastructure consistently and predictably.
    
4. **Reusability:** It allows you to define infrastructure as modular components, which can be easily reused across multiple deployments. This can help reduce duplication and make it easier to manage your infrastructure at scale.
    
5. **Portable across cloud providers:** It can be used with different cloud services, so you can manage your setup the same way no matter where it is. Terraform has many advantages for handling infrastructure as code and is a must-have tool for creating repeatable multi-cloud systems.
    

## ✔️ Important terrafrom terninologies

1. **Variables:** Terraform has input and output variables; these are key-value pairs. Input variables are used as parameters to input values at runtime to customize our deployments. Output variables are return values of a Terraform module that can be used by other configurations. Read our blog on Terraform Variables.
    
2. **Provider:** Terraform allows users to provision their infrastructure on major cloud providers such as AWS, Azure, OCI, and others. A provider is a plugin that interacts with the necessary APIs to create, update, and delete various resources.
    
3. **Module:** Any set of Terraform configuration files in a folder is a module. Every Terraform configuration has at least one module, known as its root module.
    
4. **State:** Terraform records information about what infrastructure is created in a Terraform state file. With the state file, Terraform can find the resources it created previously, supposed to manage and update them accordingly.
    
5. **Resources:** Cloud Providers provide various services in their offerings, they are referenced as Resources in Terraform. Terraform resources can be anything from compute instances, and virtual networks to higher-level components such as DNS records. Each resource has its attributes to define that resource.
    

## ✔️ Installing terraform on an ec2 instance

Here are the steps to follow when installing Terraform on an EC2 instance.

```yaml
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
# Install the HashiCorp GPG key.
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
# Verify the key's fingerprint.
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
# update packages
sudo apt update
# install terraform
sudo apt-get install terraform
```

## 📍 Conclusion

In conclusion, Terraform is a useful tool for handling infrastructure with code, offering advantages like better teamwork, version tracking, consistency, reusability, and working with different cloud providers.

In the upcoming blogs, we will be covering writing the terraform configuration file for provisioning infrastructure.