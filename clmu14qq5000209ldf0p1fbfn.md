---
title: "Mastering Terraform State Management: A Comprehensive Guide"
seoTitle: "Mastering Terraform State Management: A Comprehensive Guide"
datePublished: Fri Sep 22 2023 03:15:43 GMT+0000 (Coordinated Universal Time)
cuid: clmu14qq5000209ldf0p1fbfn
slug: mastering-terraform-state-management-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695352137509/4553b419-cf1b-42b2-88d4-5c84af37ecdd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695352533303/a2dcb863-5607-4648-a697-b9e8ad54e507.png
tags: devops, terraform, 90daysofdevops, trainwithshubham, terraweekchallenge

---

## 📍 Introduction

Hello readers! In today's blog, we will be learning about Terraform state, which stores all the changes made through Terraform to keep track of the resources created. Additionally, we will explore Terraform state commands that help us query information about various Terraform resources.

## ✔️ Importance of terraform state

The importance of Terraform state in managing infrastructure lies in several key factors:

1. **Consistency:** Terraform state ensures that infrastructure changes are applied consistently. By reading from and writing to the state file, it applies changes uniformly across all resources.
    
2. **Reliability:** The state file acts as a safety net, allowing for the recovery of infrastructure from failures or incorrect modifications. If a resource is accidentally deleted or misconfigured, Terraform can reference the state file to restore it to its previous state.
    
3. **Efficiency:** Terraform state improves performance by caching resource information. By storing data in the state file, Terraform avoids redundant queries to the underlying infrastructure, resulting in faster operations.
    

## ✔️ Local state and the state command

Terraform state files are normally stored locally i.e. in the folder where terraform is initialized. The location of the state file is specified in the Terraform configuration file.

By default, a local state file is saved as `terraform.tfstate` in the current working directory. To specify a different location for the state file, set the state configuration variable.

### 🔸 State commands

Whenever we apply our terraform changes all that is stored in the terraform state file, if we print the contents of the state file it will look something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695351138509/55b783a1-c691-4c4a-99f3-393cc846151d.png align="center")

The state file stores detailed information about the current state of the infrastructure. However, we cannot comprehend anything by simply looking at the contents of the state file. Instead, we should utilize the state commands.

1. `terraform state list:` This command shows all the resources created by terraform.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695351357276/6131fca1-f38f-4351-842e-4701ff6e7e92.png align="center")
    
2. `terraform state show <resource_name>`: This command shows the information about a specific resource.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695351659964/cd9d77c5-24dd-41b6-b5d2-3838e19902a7.png align="center")
    
3. `terraform state pull:` Prints the state file containing information about the resources.
    
4. `terraform state push:` This command updates the remote state using a local state file.
    

## ✔️ Remote state management and state locking

When we initialize Terraform in a folder, the state file is automatically created in that location. However, storing the state file in our GitHub repository or on our local system can be quite risky.

This may lead to inconsistencies in our infrastructure, as multiple people within an organization could be modifying the infrastructure using their own local Terraform state files. Consequently, this can result in the loss of infrastructure resources.

To avoid this, we use the concept of remote backend and state locking along with Terraform to store the state in an S3 bucket. With state locking, we can ensure that if one person is applying changes to the infrastructure, another person cannot change it at the same time.

### 🔸 Configuring remote backend using s3 and dynamo db

To configure a remote backend we can write a terraform file to provision a s3 bucket and dynamo db table. The configuration is as follows:

```bash
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.16.1"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "remote-backend-storage" {
  bucket = "remote-backend-s3-storage"
}

resource "aws_dynamodb_table" "remote-backend-table" {
  name         = "remote-backend-dynamodb-table"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"
  attribute {
    name = "LockID"
    type = "S"
  }
}
```

Copy the above contents in a .tf extension file and then run `terraform init` followed by `terraform apply.`

Now that the remote backend is created we can use it in our terraform project to store the state in a s3 bucket, we can specify that in our terraform.tf file where we keep all configurations related to terraform:

```bash
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.16.1"
    }
  }
  backend "s3" {

    bucket         = "remote-backend-s3-storage"
    dynamodb_table = "remote-backend-dynamodb-table"
    region         = "us-east-1"
    key            = "terraform.tfstate"
  }
}
```

After saving the following changes, run `terraform init` to initialize the backend configuration. Next, delete the `terraform.tfstate` and `terraform.tfstate.backup` files in the main directory.

Finally, run 'terraform apply'. Now, the `terraform.tfstate` file will be stored in an S3 bucket instead of being created locally.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695352467961/a603ec54-1907-4542-b246-a7c55c9a75c1.png align="center")

Instead, you can just execute `terraform state push terraform.tfstate` this will update the contents of the remote state file with the local state file.

## 📍 Conclusion

In conclusion, mastering Terraform state management is crucial for maintaining consistent, reliable, and efficient infrastructure. By understanding local and remote state management, as well as state locking, you can ensure your team collaborates effectively.