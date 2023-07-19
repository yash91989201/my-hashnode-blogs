---
title: "🤘 Rocking the Linux OS World: The Ultimate Guide to Fundamentals and Commands 🔥"
seoTitle: "Rocking the Linux OS World: The Ultimate Guide to Fundamentals"
seoDescription: "Master Linux OS with this comprehensive guide on fundamentals, commands, architecture, and unlock its versatile, open-source potential"
datePublished: Sun Jul 16 2023 15:46:41 GMT+0000 (Coordinated Universal Time)
cuid: clk5m0ke300050amp6jds7oyj
slug: rocking-the-linux-os-world-the-ultimate-guide-to-fundamentals-and-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689521458323/a08b3eeb-763b-40a7-bc7c-5d088593ab46.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689522348038/482f7b20-1a00-4b20-b5b1-b64b3f58fd82.jpeg
tags: linux, devops, 90daysofdevops, trainwithshubham, tws

---

## 🐧 Introduction

Welcome to the thrilling world of Linux OS! In this ultimate guide, we'll explore the basics of this user-friendly, open-source operating system. Prepare to embark on a journey that will turn you from a Linux beginner to a confident user, unlocking the true potential of this versatile platform. Let's dive in!

## 🤓 Is Linux a kernel or an operating system?

![Guy Confused Meme Generator - Piñata Farms - The best meme generator and  meme maker for video & image memes](https://a.pinatafarm.com/2000x1124/b177c50844/guy-confused.jpg align="left")

Starting my Linux journey, I was unsure if it was a kernel or a complete OS. After much study, I found out that <mark>Linux is technically just a kernel, but it's often used to describe a full operating system.</mark> This system includes a shell (like bash) and command-line or GUI tools for managing the system. The accurate term for this entire OS is a Linux distribution, or simply, a Linux distro. Well-known examples of Linux distributions are Ubuntu, Red Hat, and Debian.

Think of the Linux kernel as the heart of the system, responsible for managing hardware resources, coordinating tasks, and providing essential services. It acts as a bridge between the hardware and the software layers.

## 🏛️ Understanding the Linux architecture

![Basic Linux Tutorial for Begineers in details | What is linux and  Architecture of linux](https://generalnote.com/images/Linux-Tutorial/Architecture-of-Linux.jpg align="center")

The Linux operating system architecture consists of four key components: **hardware, kernel, shell, application and utilities.**

1. **Kernel:** The kernel is like the brain of an operating system. It plays a crucial role in controlling everything that happens in the Linux OS. It has different parts that work together with the hardware of the computer.
    
2. **System libraries:** these are special types of functions that are used to implement the functionality of the operating system.
    
3. **Shell:** It is an interface to the kernel which takes commands from the user and executes the kernel’s functions. We can interact with the shell with the help of a terminal, a terminal is a wrapper program that runs a shell and allows us to enter commands.
    
4. **Hardware Layer:** This layer consists of all physical devices like RAM, HDD, CPU etc.
    
5. **System Utility:** It provides the functionalities of an operating system to the user.
    

Let's take an example where a user wants to list all the contents of a folder or a directory (in the Linux world a folder is called a directory).

To list all the contents of a directory we use the command "ls" which is short for list.

When we enter the "ls" command in the terminal, the shell interprets the command and passes it to the kernel. The kernel then interacts with the hardware, such as the hard drive, to access the file system and retrieve the directory contents. Finally, the kernel sends the information back to the shell, which displays the directory contents to the user.

## 🔓 Unlocking the Matrix: Mastering Linux Commands for Ultimate Control

![Fast-typing GIFs - Get the best GIF on GIPHY](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExdm10eWV4eHdvcGtlZ3YwcWIzYmk3ZXN6MnZuN2VjZjJpbGExajNqZSZlcD12MV9naWZzX3NlYXJjaCZjdD1n/XIqCQx02E1U9W/giphy.gif align="center")

Linux commands are text-based instructions entered in the terminal, allowing users to interact with the operating system and perform various tasks. These commands range from simple ones, like creating, moving, and deleting files and directories, to more advanced ones, such as managing system processes, monitoring system resources, and configuring network settings.

*We can also specify some options also known as flags or switches which are additional parameters that modify the behavior of a command to perform specific tasks or provide more detailed information.* These options usually start with a hyphen (-) or two hyphens (--) and can be combined with the command to fine-tune its functions or output according to the user.

For example, the "ls" command, which lists the contents of a directory, can be used with the "-l" option to display a detailed, long-format listing, or the "-a" option to show hidden files. While it is possible to combine flags like "ls -al" or "ls -ltrh" some commands require you to specify flags separately.

Let us explore some basic Linux commands that will prove helpful when traversing the file system:

**ls (list):** lists all the contents in a directory. Along with the ls command we can use flags like -a, -l, -t, -r

```bash
ubuntu@ip-172-31-90-203:~$ ls -al
total 28
drwxr-x--- 4 ubuntu ubuntu 4096 Jul 16 14:40 .
drwxr-xr-x 3 root   root   4096 Jul 16 14:40 ..
-rw-r--r-- 1 ubuntu ubuntu  220 Jan  6  2022 .bash_logout
-rw-r--r-- 1 ubuntu ubuntu 3771 Jan  6  2022 .bashrc
drwx------ 2 ubuntu ubuntu 4096 Jul 16 14:40 .cache
-rw-r--r-- 1 ubuntu ubuntu  807 Jan  6  2022 .profile
drwx------ 2 ubuntu ubuntu 4096 Jul 16 14:40 .ssh
ubuntu@ip-172-31-90-203:~$
```

**pwd (print working directory):** prints the name of the directory that the user is currently in.

```bash
ubuntu@ip-172-31-90-203:~$ pwd
/home/ubuntu
```

**mkdir (make directory):** allows the user to create a new directory. Along with mkdir we can use the "-p" flag which will create sub-directories (directories within a directory) if it does not exist.

```bash
ubuntu@ip-172-31-90-203:~$ mkdir test_dir
ubuntu@ip-172-31-90-203:~$ ls -al
total 32
drwxr-x--- 5 ubuntu ubuntu 4096 Jul 16 14:42 .
drwxr-xr-x 3 root   root   4096 Jul 16 14:40 ..
-rw-r--r-- 1 ubuntu ubuntu  220 Jan  6  2022 .bash_logout
-rw-r--r-- 1 ubuntu ubuntu 3771 Jan  6  2022 .bashrc
drwx------ 2 ubuntu ubuntu 4096 Jul 16 14:40 .cache
-rw-r--r-- 1 ubuntu ubuntu  807 Jan  6  2022 .profile
drwx------ 2 ubuntu ubuntu 4096 Jul 16 14:40 .ssh
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 16 14:42 test_dir
```

**cd (change directory):** allows the user to change to a specified directory.

```bash
ubuntu@ip-172-31-90-203:~$ cd test_dir
ubuntu@ip-172-31-90-203:~/test_dir$ ls -al
total 8
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 16 14:52 .
drwxr-x--- 5 ubuntu ubuntu 4096 Jul 16 14:51 ..
```

**touch:** create a new file with a given name and extension

```bash
ubuntu@ip-172-31-90-203:~/test_dir$ touch awesome-file.txt
ubuntu@ip-172-31-90-203:~/test_dir$ ls -al
total 8
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 16 14:52 .
drwxr-x--- 5 ubuntu ubuntu 4096 Jul 16 14:51 ..
-rw-rw-r-- 1 ubuntu ubuntu    0 Jul 16 14:52 awesome-file.txt
```

**cat (concatenate):** prints the content of a given file on the screen.

```bash
ubuntu@ip-172-31-90-203:~/test_dir$ cat awesome-file.txt
Hi everyone,
this is yashraj jaiswal
It feels awesome to learn linux
```

**rm (remove):** removes the given file. With this command, we can use the "-r" flag, which removes the files recursively within a directory but do not use "-rf" which will forcefully delete the files and will not give a prompt when deleting important files.

```bash
ubuntu@ip-172-31-90-203:~/test_dir$ ls -al
total 12
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 16 14:48 .
drwxr-x--- 5 ubuntu ubuntu 4096 Jul 16 14:48 ..
-rw-rw-r-- 1 ubuntu ubuntu   71 Jul 16 14:48 awesome-file.txt
ubuntu@ip-172-31-90-203:~/test_dir$ rm awesome-file.txt
ubuntu@ip-172-31-90-203:~/test_dir$ ls -al
total 8
drwxrwxr-x 2 ubuntu ubuntu 4096 Jul 16 14:49 .
drwxr-x--- 5 ubuntu ubuntu 4096 Jul 16 14:48 ..
```

**whoami:** displays the username of the current user when this command is entered.

```bash
ubuntu@ip-172-31-90-203:~/test_dir$ whoami
ubuntu
```

## 📜 history command

While operating in Linux you can access your previously executed commands by pressing the up arrow key, but you can do much more with the history command.

You can also execute commands from your history too! Isn't that just incredible?! All you have to do is grab the command number from your history, slap an exclamation mark in front of it, hit enter, and BAM! Your command is executed just like that! 🎉.

```bash
  ubuntu@ip-172-31-90-203:~$
  230  clear
  231  ./get-logs.bash
  232  ls
  233  cat output_tmp
  234  clear
  235  vi get-logs.bash
  236  ./get-logs.bash
  237  ls /tmp
  238  clear
  239  ls
  240  cat awesome-file.txt
ubuntu@ip-172-31-90-203:~$ !233
cat output_tmp
Jul 16 14:40:14 ip-172-31-90-203 systemd[1]: Condition check resulted in 
Process error reports when automatic reporting is enabled (file watch) being 
skipped. Jul 16 14:40:14 ip-172-31-90-203 systemd[1]: Condition check resulted
```

The history feature stores commands in RAM until the user logs out, after which they are saved to ~/.bash\_history. The buffer can hold 1,000 commands, while the file can store up to 2,000 entries.

## 🕵️‍♂️ Exploring the Linux manual

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689521254751/05e66e06-357e-4710-96c0-dd336d484d1c.png align="center")

Linux man pages are a helpful documentation system that provides detailed information about commands, utilities, and system calls. They act as a reference guide, explaining how a specific command or program works, its syntax, and available options.

To access a man page, simply type "man" followed by the command or utility name in the terminal. These pages are divided into sections, making it easy to find the desired information quickly.

```bash
ubuntu@ip-172-31-90-203:~$ man ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689519906197/e5ca86d5-bc92-4c3f-bd82-1f228917a3fa.png align="center")

## 🛤️ Journey's End: Becoming a Linux Rockstar

In conclusion, the Linux OS offers a powerful, flexible, and versatile platform for users seeking to gain more control over their systems. By understanding its fundamentals, and architecture, and mastering its commands, you can unlock the true potential of this open-source operating system.

As you continue to explore and practice using Linux, you will become a rockstar in the world of computing. So, dive in and start your journey toward mastering the Linux OS, and don't be afraid to delve deeper and broaden your knowledge.

Happy learning!