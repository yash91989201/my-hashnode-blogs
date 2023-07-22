---
title: "🔐📜Understanding Access Control Lists in Linux: Fine-Grained Permissions Made Easy🔥🔥"
seoTitle: "Access Control Lists: Enhance security with fine-grained permissions"
seoDescription: "Master Linux Access Control Lists: Enhance security with fine-grained permissions using ACLs and Sticky Bits. Manage user access effortlessly"
datePublished: Thu Jul 20 2023 17:04:21 GMT+0000 (Coordinated Universal Time)
cuid: clkbejuru000c0amde38i87dy
slug: understanding-access-control-lists-in-linux-fine-grained-permissions-made-easy
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689872435138/6ad61a4c-fa6a-43ac-8c5e-ad421942ad67.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689872563646/e13a8e0b-70ff-42c3-9a1d-51ac7201daa5.jpeg
tags: devops, linux-for-beginners, 90daysofdevops, trainwithshubham, tws

---

## **📍** Introduction:

Hey there, readers! In this blog post, we're going to explore Access Control Lists and Sticky Bits in Linux. These nifty tools allow us to set up detailed permissions for our files and folders, making our Linux environment even more secure. Ready to dive in? Let's go!

## ✔ How does file ownership work in Linux?

If you're curious about how file permissions work in Linux, I've got you covered. Just check out my previous blog post, where I explained the basics of file permissions in a simple and easy-to-understand way. **Check out the blog here:** 👉 [https://yashraj-jaiswal.hashnode.dev/linux-file-permissions-explained-a-straightforward-method-for-file-handling](https://yashraj-jaiswal.hashnode.dev/linux-file-permissions-explained-a-straightforward-method-for-file-handling)

### 🔸 Traditional Linux permissions model

In Linux, when a user creates a file or directory, certain permissions are assigned by default. Typically, the user who created the file or directory receives read and write permissions, while the group that the user belongs to also gets read and write permissions. Other users are granted read-only access.

### 🔸 Limitations of traditional Linux permissions:

With traditional Linux permissions, we can only assign permissions for the user, their group, and others. Now, let's have a look at a scenario where this might be a bit restrictive.

A user named **Alice** creates a file that she wants to share with her team members **Bob** and **Carol**. However, she doesn't want to give access to other team members. With traditional Linux permissions, Alice can only set permissions for the owner (herself), group, and others. This means *she cannot specifically grant access to just Bob and Carol without adding them to a new group or giving access to everyone in her current group.*

## ✔ Introduction to Linux ACLs

An **Access Control List** (ACL) in Linux is a set of extended permissions that offer finer control over file and directory access beyond the traditional **user, group,** and **others** permissions model. ACLs enable administrators to grant or deny particular users and groups access to files and directories, providing flexibility and granularity in managing permissions.

Let's examine how ACLs can assist us in addressing the situation described in the previous section:

With ACLs, Alice can grant particular permissions to Bob and Carol without impacting the access of other users or groups.

```bash
setfacl
```

## ✔ Using ACLs in Linux

To implement Access Control Lists (ACLs) in Linux, we can utilize two specific commands which are getfacl and setfacl.

You may encounter an error when attempting to execute the getfacl or setfacl commands. If this occurs, simply install the acl package by entering the following command: `sudo apt install acl`

### 🔸 Viewing existing ACLs with getfacl

The getfacl command enables users to retrieve and display the current ACL settings for a specific file or directory. The getfacl command presents the permissions applied to a file in a clear and organized manner.

```bash
ubuntu@learn-linux:~$ ls
ping-output  scripts
ubuntu@learn-linux:~$ getfacl scripts
# file: scripts
# owner: ubuntu
# group: ubuntu
user::rwx
group::rwx
other::r-x
```

### 🔸 Modifying ACLs with setfacl

We can use the setfacl command with different options to apply fine-grained permissions to a file or directory. A basic syntax for setfacl command is as follows: `setfacl -m "u:user:permissions" /path/to/file` and for groups `setfacl -m "g:group:permissions" /path/to/file`

1. Add execute permission to a user named bob.
    
    ```bash
    setfacl -m u:bob:x /home/ubuntu/scripts/create_backup.sh
    ```
    
2. Remove read and write permission for a user named bob.
    
    ```bash
    setfacl -x u:bob:rw /home/ubuntu/scripts/check_disk_space.sh
    ```
    
3. Allow all files and directories to inherit ACL permission from the directory it's within.
    
    ```bash
    # this will allow all the files within scripts to inherit 
    # the same ACL permissions given to scripts folder
    setfacl -dm u:alice:rwx /home/ubuntu/scripts
    ```
    
4. Remove all ACL entries from a file
    
    ```bash
    setfacl -b /home/ubuntu/scripts/create_backup.sh
    ```
    
5. Add permission to a group
    
    ```bash
    setfacl -dm g:ubuntu:r /home/ubuntu/scripts
    ```
    

## ✔ Sticky Bit: Prevent your files from being deleted😎

Sticky Bit is a security feature that restricts file or directory deletion and renaming, allowing only the file owner or directory owner to perform these actions.

The sticky bit is represented by a T (when execute permission is not given to the file or directory or file) or t (when execute permission has already been applied)

```bash
# before setting sticky bit 
ubuntu@learn-linux:~$ ls -al | grep scripts
drwxrwxr-x 3 ubuntu ubuntu  4096 Jul 20 10:05 scripts
# after setting sticky bit 
ubuntu@learn-linux:~$ chmod o+t scripts 
ubuntu@learn-linux:~$ ls -ltr | grep scripts
drwxrwxr-t 3 ubuntu ubuntu 4096 Jul 20 10:05 scripts
```

## **📍** Conclusion:

So, to sum it all up, Access Control Lists (ACLs) in Linux are super handy for managing file and directory permissions with more precision than the old-school method. By using the getfacl and setfacl commands, admins can easily and smoothly grant or deny access to certain users and groups. This way, we can keep our Linux environment safe, secure, and well-organized. 😊