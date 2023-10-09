---
title: "🏗️ Deploying WordPress on AWS with RDS as database 💾"
seoTitle: "🏗️ Deploying WordPress on AWS with RDS as database 💾"
datePublished: Mon Oct 09 2023 17:29:04 GMT+0000 (Coordinated Universal Time)
cuid: clnj63mxv00030al70ogq64mq
slug: deploying-wordpress-on-aws-with-rds-as-database
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696870008408/c1108124-057a-423b-8e89-376ad8c60be5.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1696870019500/7000f6ed-56e3-4863-9b95-0545295bb2d4.png
tags: devops, aws-rds, 90daysofdevops, aws-projects, trainwithshubham

---

## 📍 Introduction

Hello readers! In this blog, we will be constructing an AWS project in which we will host a WordPress website using RDS as the database. If you are interested in learning how to create a database on RDS, please refer to [this blog post](https://yashraj-jaiswal.hashnode.dev/managed-relational-database-service-in-aws).

### 🔸 Step 1: Create a MySQL RDS database.

Create an RDS instance with the following configurations.

1. First we select MySQL as the database engine.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696865790136/c5d7b355-f620-4e0b-9a78-ea9c27a40279.png align="center")
    
2. Then select the free tier for the project
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696865818327/f3f6ecdc-f4cf-433f-a50b-14c8828e4ccb.png align="center")
    
3. Now, set up the admin credentials for the database. Remember these credentials, as they will be crucial for connecting our RDS instance to WordPress.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696865851202/ef6f1df6-19e5-4d19-8386-8fd107ec06da.png align="center")
    
4. Now for storage options select the gp3 storage option type as it is more performant.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696865965284/aebf363c-29dc-41e0-b2be-4ec5fd034a75.png align="center")
    
5. In the connectivity section, choose public access to obtain a public endpoint, which will enable us to access the database for both reading and writing purposes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696866103371/ebf94f5e-daa9-4b91-813c-da5ec45f28cb.png align="center")
    
6. Set database connection as password authentication.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696866145336/90ef0c5b-a6c9-4ebc-a75a-edc7d75aace6.png align="center")
    
7. Now in the additional section add a name for the initial database.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696866197651/48f2787b-4dbd-4f90-939d-46f215fff160.png align="center")
    
8. Click on `Create Database` and wait for it to start running. The database will be provisioned within 15 minutes.
    

### 🔸 Step 2: Create EC2 instance and install WordPress

1. Provision an EC2 instance and connect to it using SSH (make sure that the security group allows access through port 80).
    
2. Install apache webserver using the following command:
    
    ```bash
    # update packages
    sudo apt update
    # install apache webserver
    sudo apt install apache2
    # start apache server
    sudo systemctl start apache2
    ```
    
3. Download WordPress.
    
    ```bash
    wget https://wordpress.org/latest.tar.gz
    tar -xzf latest.tar.gz
    
    cd wordpress
    cp wp-config-sample.php wp-config.php
    ```
    
4. Now we need to edit the database configuration so we can connect it to our RDS instance. Edit the following values with the values from the RDS instance we just created.
    
    ```bash
    // ** MySQL settings - You can get this info from your web host ** //
    /** The name of the database for WordPress */
    define( 'DB_NAME', 'database_name_here' );
    
    /** MySQL database username */
    define( 'DB_USER', 'username_here' );
    
    /** MySQL database password */
    define( 'DB_PASSWORD', 'password_here' );
    
    /** MySQL hostname */
    define( 'DB_HOST', 'localhost' );
    ```
    
5. Now change the authentication with these values. You can generate the values from [here](https://api.wordpress.org/secret-key/1.1/salt/).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696868208102/e39f0216-2c51-45af-9685-9ab27aafa307.png align="center")
    

### 🔸 Step 3: Configure your RDS instance to connect with WordPress.

1. Install MySQL on EC2 instance.
    
    ```bash
    sudo apt update
    sudo apt install mysql-server
    ```
    
2. Configure environment variable.
    
    ```bash
    export MYSQL_HOST=<rds endpoint>
    ```
    
3. Connect to MySQL RDS instance and configure database for WordPress.
    
    ```bash
    # execute the command and enter admin password when prompted
    mysql -h <RDS endpoint> --user <RDS admin user> -p
    ```
    
    Then execute the following SQL commands.
    
    ```sql
    CREATE DATABASE wordpress_db
    CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
    GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
    FLUSH PRIVILEGES;
    EXIT
    ```
    

### 🔸 Step 4: Deploying WordPress website.

1. Install the required dependencies for deploying WordPress.
    
    ```bash
    sudo apt update
    sudo apt install php8.1
    ```
    
2. Copy the WordPress directory to `/var/www/html` directory. Restart the Apache server. If restarting the Apache web server does not work for you, try stopping and starting the EC2 instance.
    
    ```bash
    # navigate to the directory where you downloaded wordpress
    sudo cp -r wordpress/* /var/www/html/
    # restart the apache webserver
    sudo systemctl restart apache2
    ```
    
3. Now you can view the deployed WordPress website using the IP address of the ec2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696872456407/0e7231d3-a5a3-469e-ad24-32370fde2073.png align="center")
    
    Now fill out some details and then click on Install WordPress. Then login using the created user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696872514218/7a02fd0a-26d5-4893-a61c-2f75b087abff.png align="center")
    
4. Once the project is completed, be sure to delete all provisioned resources, such as RDS and EC2 instances, to prevent incurring any additional costs.
    

## 📍 Conclusion

In this tutorial, we have successfully deployed a WordPress website on an AWS EC2 instance and connected it to an RDS MySQL database. By following these steps, you can easily set up your WordPress site on AWS, ensuring scalability and flexibility for your project.

While this is a simple project, we are just beginning, in upcoming blogs we will be doing amazing projects on AWS and DevOps so stay tuned and keep upskilling.