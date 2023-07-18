---
title: "Introduction to Linux Shell Scripting: Getting Started with the Basics 🔥"
seoTitle: "Linux Shell Scripting Basics: Intro Guide"
seoDescription: "Learn Linux shell scripting basics: commands, variables, conditionals for efficient system administration in this introductory guide"
datePublished: Tue Jul 18 2023 18:27:37 GMT+0000 (Coordinated Universal Time)
cuid: clk8mn84h00000ajm65qh5d5a
slug: introduction-to-linux-shell-scripting-getting-started-with-the-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689704441303/07dba51f-c6be-405e-9778-41cfb124b122.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689704844410/b191e7f2-0285-4163-8954-d74462ce5afd.png
tags: linux, devops, linux-for-beginners, 90daysofdevops, trainwithshubham

---

## **📍**Introduction:

Hello readers! In today's blog about the Linux shell, we will be exploring the basics of shell scripting, its importance in Linux administration, and how to get started with various shell commands and scripting techniques. Sounds awesome, right? Let's dive in!

## **✔**What is a Linux shell?

Whenever a user logs in to the system or opens a console window, the kernel runs a new shell instance. It is responsible for the control management, and execution of processes, and ensuring proper utilization of system resources.

A shell is a program that serves as an interface between a user and the kernel. It enables a user to issue commands to the kernel and receive responses from it. Through a shell, we can execute programs and utilities on the kernel. Therefore, at its core, a shell is a program designed to execute other programs on our system.

Being able to interact with the kernel makes shells a powerful tool. Without the ability to interact with the kernel, a user cannot access the utilities offered by their machine’s operating system.

Let’s understand the major shells that are available for the Linux environment.

1. **The Bourne shell (sh):** The first UNIX shell, called Bourne shell or sh, was made by Steve Bourne at AT&T Bell Labs. It's small and fast, so it became the main shell for Solaris OS and its admin scripts.
    
2. **The GNU Bourne-Again Shell (bash):** More commonly known as the Bash shell, the GNU Bourne-Again shell was designed for compatibility with the Bourne shell. It includes helpful features from various Linux shells, such as the Korn shell and C shell. It allows us to automatically recall previously used commands and edit them with the help of arrow keys, unlike the Bourne shell.
    
    The complete path name for the GNU Bourne-Again shell is /bin/bas
    
3. **The Korn Shell (ksh):** The Korn shell was developed at AT&T Bell Labs by David Korn to improve the Bourne shell. It is denoted as ksh. Essentially, the Korn shell is a superset of the Bourne shell.
    
4. **The Z Shell (ssh):** The Z Shell or zsh is a sh shell extension with tons of improvements for customization. If you want a modern shell that has all the features a much more, the Zsh shell is what you’re looking for.
    

## **✔** Shell Scripting:

![Should you learn Linux shell commands as a web developer in 2023? - DEV  Community](https://res.cloudinary.com/practicaldev/image/fetch/s--kcdpxq9a--/c_imagga_scale,f_auto,fl_progressive,h_900,q_auto,w_1600/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7fvwgm9uml3vthyp61kq.png align="left")

A shell script is a text file that contains a sequence of commands that are typed in the terminal and is mostly used to automate those tasks that are needed to be performed repeatedly. A shell script is a text file that puts together many Linux commands.

Like other programs, the shell script can contain parameters, comments, and subcommands that the shell must follow. Users initiate the sequence of commands in the shell script by simply entering the file name on a command line.

After writing a shell script, we also need to grant the script execute permissions so that it can be executed in the command line.

### 🔸 How to write a shell script?

A shell script must always start with **the shebang** `#/bin/sh` or `#!/bin/bash`. This is very important as it tells the kernel which interpreter is to be used to run the commands present in the file.

You can include Linux commands like ls, pwd, whoami, hostname in a shell script

Here's an example of a shell script

```bash
#!/bin/bash
echo This is my first shell script 
touch test_file
ls
echo End of my shell script

output: 
This is my first shell script
DevOps   ec2key.pem   hello.bash   test_file   testscript   WebDev
End of my shell script
```

### 🔸 Adding comments in a shell script:

To add a comment in shell script we just use the pound or hash symbol before the specific line and that will be ignored by the interpreter.

```bash
#!/bin/bash
# This is a comment
echo Testing comments in shell script

output:
Testing comments in shell script
```

### 🔸 Executing a shell script:

By default, a newly created script does not have execute permissions, so attempting to execute it will result in an error. To execute a shell script, we first need to modify its permissions using the `chmod` command.

After modifying the permissions the script is ready to be executed.

```bash
ubuntu@ip-172-168-29-30:~$ chmod u+x test_script.sh
ubuntu@ip-172-168-29-30:~$ ls -l test_script.sh
-rwxrw-r-- 1 ubuntu 197121 34 Jul 18 12:16 test_script.sh
ubuntu@ip-172-168-29-30:~$ ./test_script.sh
Testing comments in shell script
```

### 🔸 Using variables in a shell script:

Variables in shell scripts are important for storing and manipulating data. They offer a method to assign values to a named symbol and reference that value throughout the script. By utilizing variables, we can create more dynamic and adaptable scripts. They enable us to store user input, intermediate results, or system-generated values.

Check out this example of using a variable in a shell script.

```bash
NAME="yash"
echo $NAME

output:
yash
```

On executing the above script it will print "yash" on the screen

## **✔** Command substitution:

Command substitution is a way for programmers to use the result of a command in place of the command itself in shell scripts. The shell runs the command and replaces the substitution with the command's output. The output of a UNIX command is packaged and then used as a command.

This might seem a bit tricky at first, but let's make it easier by going through an example together:

There are 2 ways of command substitution:

1. **Using $():** when using $() it provides flexibility as we can nest $() within itself.
    

```bash
file_owner=$(ls -l /home/ubuntu/test_script.sh | awk '{print $3}')
echo "The file is owned by $file_owner"

output:
The file is owned by ubuntu
```

1. **Using backticks \`\` :**
    

```bash
file_count=`ls -l | grep '^-' |wc -l`
echo "$(pwd | awk -F/ '{$print $NF}') folder has $(file_count) files"

output:
scripts folder has 5 files
```

## **✔** Conditional statements:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689704643039/173af616-5e18-498f-98c1-358936d702d7.png align="center")

As the name implies, conditional statements allow the execution of different sets of instructions depending on the evaluation of particular conditions. These conditions are typically expressed as logical expressions, which can be true or false. When a specific condition is met, the corresponding block of code is executed. This allows for the implementation of decision-making processes and the handling of various scenarios within the code.

There are 5 types of conditional statements

1. if statement
    
2. if-else statement
    
3. if..elif..else..fi statement (Else If ladder)
    
4. if..then..else..if..then..fi..fi..(Nested if)
    
5. switch statement
    

```bash
if [ expression ]
then
   statement
fi
```

Expressions can be of the following type

| Integer Comparisons | Function |
| --- | --- |
| **\-gt** | Greater-than |
| **\-lt** | Less-than |
| **\-ge** | Greater-than-or-equal-to |
| **\-le** | Less-than-or-equal-to |
| **\-eq** | Equal |
| **\-ne** | Not-equal |
| **String Comparisons** |  |
| **\-z** | Tests for empty string |
| **\=** | Equal strings |
| **!=** | Not-equal strings |
| **Logical Operations** |  |
| **\-a** | Logical AND |
| **\-o** | Logical OR |
| **!** | Logical NOT |
| **File Tests** |  |
| **\-f** | File exists and is a regular file |
| **\-s** | File is not empty |
| **\-r** | File is readable |
| **\-w** | File can be written to, modified |
| **\-x** | File is executable |
| **\-d** | File name is a directory name |

Let's create a fun example to make a backup of the /var and /etc file systems if they don't already exist in the /tmp directory.

```bash
#!/bin/bash
cd /tmp
backup_file=`ls -ltr | grep '$*.tar.gz' | wc -l`
backup_date=`date +"%d_%m_%y"`
if [ $backup_file -eq 0 ]
then
    echo Creating a backup file
    tar cvf /tmp/backup_$backup_date.tar /var /etc &> /dev/null
    echo Compressing Backup file
    gzip /tmp/backup_$backup_date.tar
    echo Backup successful
else
    echo Backup already taken
fi
```

## **📍** Conclusion:

In conclusion, Linux shell scripting is a powerful tool for automating tasks and managing system resources. By understanding the basics of shell commands, scripting techniques, and control structures, you can harness the full potential of Linux administration and simplify your daily tasks.

As you continue to learn and practice, you'll find shell scripting to be an invaluable skill in your toolkit.

Happy Learning!