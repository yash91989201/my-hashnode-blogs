---
title: "Linux File Permissions Explained: A Straightforward Method for File Handling 📁"
seoDescription: "Master Linux file permissions for security; learn read, write, execute with chmod in symbolic, octal modes"
datePublished: Mon Jul 17 2023 17:48:22 GMT+0000 (Coordinated Universal Time)
cuid: clk75swic00060alcaqj8fvvr
slug: linux-file-permissions-explained-a-straightforward-method-for-file-handling
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689615776169/2404fcd2-25ba-4b88-bf0d-fe27243b24c6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689616075152/71be44cf-2d63-4f80-a95f-fd3063c7a89a.png
tags: devops, linux-for-beginners, file-permission, 90daysofdevops, trainwithshubham

---

## Introduction

Welcome, dear readers! Are you ready to embark on an exciting journey to discover the world of Linux file permissions? By understanding and mastering this powerful concept, you'll unlock a new level of security and control over your files and directories. So, let's dive in and explore the fascinating world of Linux file permissions together!

## What are file permissions? 🔒

File permissions in Linux are an incredible concept! Thanks to these amazing file permissions, Linux has become one of the most secure operating systems out there!

Linux file permissions provide a fine-grained access control mechanism. Each file and directory has permissions associated with it, determining who can read, write, or execute the file. By setting appropriate permissions, you can restrict access to sensitive files and directories, allowing only authorized users or groups to interact with them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689615483361/9d70d347-68f5-497a-8f47-9c792da0b92d.png align="center")

File permissions enable the separation of user data and system files. Each user has their home directory with specific permissions, ensuring that user files remain isolated and protected from other users. This prevents unauthorized access or modification of personal data.

**Here's how you can view the permissions of a Linux file:**

The "ls" command can be used to list all files along with their permissions.

```bash
ubuntu@ip-172-31-90-203:~$ ls -l
total 16
-rw-rw-r-- 1 ubuntu ubuntu    0 Jul 16 14:46 awesome-file.txt
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 16 14:52 test_dir
drwxrwxr-x 3 ubuntu ubuntu 4096 Jul 17 02:50 logs
-rw-rw-r-- 1 ubuntu ubuntu   57 Jul 17 15:59 fruits.txt
-rw-rw-r-- 1 ubuntu ubuntu   51 Jul 17 16:01 colors.txt
```

The -l flag is to print the long list format, this prints the file name along with its permission as well.

Let's understand how to read Linux file permission:

![Deciphering Linux File System Permissions - Pressidium Hosting](https://pressidium.com/wp-content/uploads/2017/02/Pressidium_blogpost_23_02_2017_Blog-post-1.png align="left")

The **first set** of permissions applies to the owner of the file. The **second set** of permissions applies to the user group that owns the file. The **third set** of permissions is generally referred to as "others." All Linux files belong to an owner and a group.

1. **Read (r):** The read permission enables you to open and view the contents of a file. However, it does not allow you to make any edits or modifications to the file.
    
2. **Write (w):** The write permission enables you to edit, delete, or rename a file. For example, if a file is located in a directory and has write permission enabled but the directory does not, you can modify the file's content but cannot delete or rename it.
    
3. **Execute (x):** In Unix type system, you can't run or execute a program unless execute permission is set. But in Windows, there is no such permission available.
    

These file permissions can also be represented in numbers and are called numeric mode. In numeric mode, a three-digit value represents specific file permissions (for example, 754.) These are called octal values. The first digit is for owner permissions, the second digit is for group permissions, and the third is for other users. Each permission has a numeric value assigned to it:

* read (r): 4
    
* write (w): 2
    
* execute(x): 1
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689613801629/80db40f7-c154-476e-93c7-7b0ee559b227.png align="center")

Above is a file with read, write, and execute permissions for the user who created it; read and execute permissions for the group the user belongs to; and read-only permission for others.

## Changing permission for a file: using the chmod command

The chmod command is used to change the access mode of a file. The name is an abbreviation of "change mode," which indicates that every file and directory has a set of permissions controlling who can read, write, or execute the file.

In this case, the permissions fall into three categories: read, write, and execute, represented by the letters r, w, and x, respectively. These letters combine to form specific permission for a group of users.

Here's the syntax for the chmod command :

`chmod [options] [mode] [File_name]`

Let's understand with an example:

```bash
ubuntu@ip-172-31-90-203:~$ ls -l config.yml
-rw-rw-r-- 1 ubuntu ubuntu 51 Jul 17 16:01 config.yml
```

In the example above, the file "config.yml" has read-and-write permissions for the user, read-and-write permissions for the user group, and read-only permission for others.

This is a configuration file, and you are instructed to grant the user read and write permissions for the file. How would you do it?

There are two ways to go about it:

1. **Symbolic mode:** In symbolic mode, which is the most common method for specifying permissions, we create a combination of letters and operators to define or modify the permissions.
    

```bash
chmod u+rw config.yml
```

1. **Octal mode:** It is also a method for specifying permissions. In this method, we specify permissions using a three-digit number. The first digit specifies the permission for the owner, the second digit specifies the permission for the group, and the third digit specifies the permission for others.
    

```bash
chmod 600 config.yml
```

## Conclusion

In conclusion, Linux file permissions are vital for guaranteeing the security and integrity of your precious files and directories! By mastering and managing these permissions with super cool commands like chmod, you'll be completely in charge of who can peek, tweak, and run your files, boosting the safety of your entire system to new heights!

Hey there! I hope you enjoyed going through this guide on Linux file permissions and found it easy to follow. I'm eager to hear your thoughts, the amazing experiences you've had, and any questions that might be on your mind. Let's continue our fantastic journey in the world of Linux, hand in hand!

Happy learning!