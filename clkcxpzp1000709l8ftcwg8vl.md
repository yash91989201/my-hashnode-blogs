---
title: "🛣️A guide to managing services and packages in Linux. 🚀"
seoDescription: "Master Linux services/packages management with our guide, covering key concepts, best practices, and tools for an optimized experience"
datePublished: Fri Jul 21 2023 18:48:46 GMT+0000 (Coordinated Universal Time)
cuid: clkcxpzp1000709l8ftcwg8vl
slug: a-guide-to-managing-services-and-packages-in-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689965118868/52262733-4a87-4a08-8b7b-5907d0c18868.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689965305148/7110bd24-869b-4c24-833c-628df7456410.png
tags: linux, devops, linux-for-beginners, 90daysofdevops, trainwithshubham

---

## **📍** Introduction:

Welcome to our guide on managing Linux services and packages! In this blog, we will cover essential concepts, best practices, and tools to simplify the process. Regardless of your experience level, we will help you enhance your Linux experience. Let's unleash the true potential of your Linux environment.🚀

## Understanding Processes, Daemons, and Services:

1. **processes:** A process is a program in execution. For example, when we write a program in C or C++ and compile it, the compiler creates binary code. The original code and binary code are both considered programs. When we run the binary code, it becomes a process.
    
    A process is an 'active' entity, as opposed to a program, which is considered a 'passive' entity. Keep in mind that a user needs to run an application or command for a process to start.
    
2. **daemons:** A daemon is a type of process that operates in the background, independent of the user interface. Typically initiated during system boot, daemons continue to run until the system is shut down. They are designed to manage periodic service requests, which they execute autonomously. A daemon process always ends in **d** like systemd, sshd, httpd, and many more.
    
3. **services:** In the context of Ubuntu, the term service often refers to a daemon or group of daemons that provide specific functionality. Services are background processes that are designed to run continuously, providing functionality to other programs or users.
    
    Services can be started, stopped, and managed independently of user sessions. Examples of services include web servers (like Apache), database servers (like MySQL), and file-sharing applications (like Samba).
    

### systemd (one daemon to rule them all 🧙‍♂️):

Systemd is the master daemon in Linux, serving as the initial daemon responsible for starting all other processes. It functions as both a service manager and an initialization system within the Linux operating system.

As systemd is the first process to start in Linux, it has a process ID of 1, and all other processes trace their origins back to it. This can be observed by using the `pstree` command, which displays the process tree.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689958087382/f0a0a654-f76d-405d-884d-9d35e3563cea.png align="center")

Systemd is a Linux initialization system that is started directly by the kernel. All other processes are either initiated directly by systemd or by one of its child processes. When systemd interacts with a daemon, it refers to them as units.

## Managing services with systemctl command :

While systemd functions as a service manager and initialization system, systemctl is a command-line tool that enables the management and monitoring of the systemd system and service manager. systemctl stands for system control.

Here's how we can use the systemctl command to manage services:

1. **starting and stopping services:** to stop a service use `systemctl stop sshd` `systemctl start sshd` . After stopping sshd service you can use the `systemctl status sshd` to check the status of sshd.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689959894727/01650de5-50d8-4e5b-a0d7-f4f462b0a315.png align="center")

1. **restarting vs reloading a service:** When it comes to restarting versus reloading a service, restarting involves terminating the service and then starting it again. On the other hand, reloading is useful when you have modified the configuration files of a daemon and only need to refresh the updated config files.
    
    Since reloading only updates the configuration, it causes minimal disruption to ongoing activities and currently open connections. Users may not even notice that the command was executed.
    
    But reload may not work on some daemons, so what's the solution; why not use both `systemctl reload-or-restart sshd` which will first try to reload and if it fails then it will restart the given service.
    
2. **enabling and disabling a service:**
    
    A service can be set to run when the system starts by enabling it. To achieve this, use the command `systemctl enable service_name`. If you want to prevent the service from starting on startup, you can disable it with the command `systemctl disable service_name`. To enable it again, simply use `systemctl enable service_name`
    
3. **masking a service:** When a service is masked, it becomes "impossible" to load the service, even if another enabled service requires it. If you want to ensure a service never starts again, mask it by executing the command `systemctl mask service_name`.
    

## Linux Packages

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689963895146/db25e30b-3de9-4447-b9bb-770d3ad433e7.png align="center")

**Packages** in Linux are collections of files and metadata that contain software applications and their dependencies. They play a crucial role in simplifying software installation, management, and updates, as they allow users to easily install, update, or remove applications on their system using package management tools like APT and YUM.

**Repositories** hold packages specifically designed, compiled, and maintained for each Linux version and distribution. These repositories house thousands of packages produced by the distribution vendors. Occasionally, projects may manage their packaging and distribution.

### Package management tools:

1. **Advanced Package Tool (APT):** APT (Advanced Package Tool) is a powerful package management system used primarily in Debian-based Linux distributions, such as Debian itself, Ubuntu, Linux Mint, and many others. It simplifies the process of installing, updating, and removing software packages on your system, making it a crucial tool for both regular users and system administrators.
    
2. **Yellodog Updater Modified (YUM):** Yum (Yellowdog Updater Modified) is a package management tool used primarily in Red Hat-based Linux distributions, including CentOS, Fedora, and RHEL (Red Hat Enterprise Linux). Yum also simplifies the process of installing, updating, and removing software packages on your system.
    

### Package management using APT:

![APT Package Manager on Linux Explained – devconnected](https://devconnected.com/wp-content/uploads/2019/11/featured-9.png align="left")

1. **Installing a package:** To install packages using APT, you can use the following command:
    
    ```bash
    sudo apt install package_name
    ```
    
    Replace `package_name` with the name of the package you want to install.
    
2. **Uninstalling a package:** Enough talk about installing packages, let’s see how to remove packages. Removing packages is as easy as installing them. Just use the command below:
    
    ```bash
    sudo apt remove package_name
    ```
    
3. **Updating package database:** apt works on a database of available packages. If the database is not updated, the system won’t know if there are any newer packages available. This is why updating the repository should be the first thing to do in in any Linux system after a fresh install. To update the package database use the following command `sudo apt update`
    
4. **Upgrading the packages:** Once you have updated the package database, you can now upgrade the installed packages. The most convenient way is to upgrade all the packages that have available updates. To upgrade the packages we can use the following command **sudo apt upgrade**
    

### Difference between upgrade and update:

![Difference between Update and Upgrade - GeeksforGeeks](https://media.geeksforgeeks.org/wp-content/uploads/20220131115605/updatevsupgrade.png align="left")

Even though the apt update command might seem like the obvious go-to option to update your packages on Linux, it's not entirely the case. The update command informs you about the available updates, but it does not download or install the updates within your distro.

On the other hand, the apt upgrade command downloads and installs available updates on your machine in one go. Your Linux system has a cache of available software (packages), which contains the necessary metadata related to those packages. The metadata includes information about the version, repository, dependency, and other relevant package details.

If you don't use the update command, you won't refresh the cache, which would not provide you with information about the available package updates.

## **📍** Conclusion: