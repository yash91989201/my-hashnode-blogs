---
title: "🔥Advanced shell scripting: Elevate your Linux skills📈 (Part - 1)"
seoTitle: "Advanced Shell Scripting: Enhance Linux (Pt.1)"
seoDescription: "Master Linux shell scripting, case statements, loops, seq, cron jobs, I/O redirection, pipe operator; enhance efficiency, automate tasks"
datePublished: Wed Jul 19 2023 18:59:21 GMT+0000 (Coordinated Universal Time)
cuid: clka37w0v000309mg5sut1ebj
slug: advanced-shell-scripting-elevate-your-linux-skills-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689793076313/b515cd29-6a75-4153-9ec3-68c0c7aa0544.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689793094504/b500bc38-55c9-432b-9680-ae7f82782e71.png
tags: linux, devops, 90daysofdevops, trainwithshubham, tws

---

## **📍** Introduction

Hey there, amazing readers! 🎉 Get ready for a thrilling adventure as we plunge headfirst into the fantastic world of Linux shell scripting! 🚀 We'll uncover the secrets of advanced Linux concepts and have a blast doing it! Let's go! 🌟.

## 👉 Prerequisites:

To follow along with this blog, you need to have a basic understanding of shell scripting and how it functions. You can find a brief introduction to shell scripting in one of my previous blog posts; Check it out here 😁 -&gt; [https://yashraj-jaiswal.hashnode.dev/introduction-to-linux-shell-scripting-getting-started-with-the-basics](https://yashraj-jaiswal.hashnode.dev/introduction-to-linux-shell-scripting-getting-started-with-the-basics)

## ✔ Shell scripting advanced concepts

### 🔸 Case statements:

A case statement in Bash scripts is used when a decision must be made among multiple choices. In other words, it is helpful when an expression can have various values. This approach can be seen as a substitute for multiple if-statements in a script.

Case statements have an advantage over if statements because they enhance the readability of our code and are easier to maintain. A case statement begins with the `case` keyword which is followed by an expression and the in the keyword and ends with the `esac` keyword

Let's explore case statements together by checking out a fun example, where we write a shell script that allows a user to input a file name and perform some actions on it :

```bash
#!/bin/bash
echo Name the file you want to operate on 
read fileName
echo Select an option from the following
echo 1) Read file contents
echo 2) Update file contents
echo 3) Delete file
echo -n "Enter your choice: " 
read ch

case #ch in 
    1) cat $fileName ;;
    2) 
        echo Enter contents that you want to append to the file
        read content
        echo $content >> $fileName
        ;;
    3) rm $fileName ;;
    *) echo Invalid Choice
esac
```

In the example above, we have created a bash script that enables the user to input the name of the file they wish to manipulate. The user is presented with several options to choose from.

Given the multiple choices, the case statement is considered appropriate for use in this situation.

### 🔸 Looping statements:

A loop is an essential programming tool. It enables you to repeatedly execute a set of commands. This allows for running a command or a series of commands multiple times.

There are 3 types of looping statements:

1. **while loop:** A while loop evaluates a condition and executes the statements within the loop as long as the condition remains true. It is commonly used when the number of times the loop needs to be executed is unknown.
    
    ```bash
    #!/bin/bash
    i=1
    while [ $i -le 10 ]
    do
        echo $i
    	i=`expr $i + 1`
    done
    ```
    
2. **for loop:** The for loop is useful in situations where we need the loop to execute a specific number of times.
    
    ```bash
    #!/bin/bash
    for num in {1..10}
    do
        echo $num
    done
    ```
    
3. **until loop:** The until loop is somewhat similar to the while loop. However, what sets them apart is that the until loop executes the body of the loop until the conditional statement returns true.
    
    ```bash
    #!/bin/bash
    x=0
    until [ $x -eq 10 ]
    do
      echo "Value of x is $x"
      x=$(($x+1))
    done
    echo "Loop ends"
    ```
    

### 🔸 Sequence Expression:

The Bash sequence expression generates a range of integers or characters by defining the start and the end point of the range. It is generally used in combination with "for" loops. Following is the syntax of sequence expression `{START..END[..INCREMENT]}`

Here are various examples to help you better understand the concept:

```bash
# print number from 1 till 3 
for $i in {1..3}
do 
    echo $i
done

output:
1
2
3

# print even number from 1 to 10
for $i in {2..10..2}
do
    echo $1
done

output:
2
4
6
8
10
```

### 🔸 seq command:

`seq` command in Linux is used to generate numbers from FIRST to LAST in steps of INCREMENT. It is a very useful command where we had to generate a list of numbers in while, for, and until loop. Here's the syntax for `seq` command `seq [option] FIRST INCREMENT LAST`

Let's examine some examples to gain a better understanding of how this functions:

```bash
seq 10 # prints from 1 to 10
seq 5 10 # prints from 5 to 10
seq 2 2 10 # prints 2 4 6 8 10
```

### 🔸 Cron:

The cron command-line utility is a job scheduler for Unix-like operating systems. Users who set up and maintain software environments utilize cron to schedule jobs (i.e., commands or shell scripts), also known as cron jobs, to run periodically at fixed times, dates, or intervals.

A cron job is a command run by the cron daemon at regularly scheduled intervals. It primarily automates system maintenance or administration, though its general-purpose nature makes it useful for tasks such as downloading files, creating backups, and checking system status.

### 🔸 crontab command in Linux:

`crontab` is a command that creates a table or list of commands, each of which is to be executed by the operating system (OS) at a specified time and on a regular schedule. `crontab` is used to create the crontab file and later used to change the previously created crontab file.

The crontab command has the following flags:

* **crontab -e** – used to edit system crontabs. This command will create a new crontab if it has not been made yet.
    
* **crontab -l** – used to view crontab entries (cron jobs) and display system crontab file contents.
    
* **crontab -r** – will remove the current crontab file.
    
* **crontab -i** – will show a prompt before removing a user’s crontab. Highly recommended to use it together with the **\-r** flag, making the flag **\-ri**.
    

Here's an example of a crontab file(/etc/crontab):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689782999315/c5068782-4040-4226-824c-83f598998d29.png align="center")

A crontab file has 5 fields:

![How to Use the Cron Job Format to Schedule Task in Linux](https://linuxiac.b-cdn.net/wp-content/uploads/2020/10/cron-job-format.png align="left")

<table><tbody><tr><td colspan="1" rowspan="1" colwidth="200"><p><strong>Field</strong></p></td><td colspan="1" rowspan="1"><p><strong>Possible values</strong></p></td></tr><tr><td colspan="1" rowspan="1" colwidth="200"><p>Minute</p></td><td colspan="1" rowspan="1"><p>0-59</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="200"><p>Hour</p></td><td colspan="1" rowspan="1"><p>0-23</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="200"><p>Day of month</p></td><td colspan="1" rowspan="1"><p>1-31</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="200"><p>Month</p></td><td colspan="1" rowspan="1"><p>1-12</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="200"><p>Day of week</p></td><td colspan="1" rowspan="1"><p>0-6. 0 depicts Sunday. In some systems, a value of 7 represents Sunday instead.</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="200"><p>Command</p></td><td colspan="1" rowspan="1"><p>Command to execute.</p></td></tr></tbody></table>

In addition to the possible values for crontab fields, it is important to remember some special characters:

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Symbol</strong></p></td><td colspan="1" rowspan="1"><p><strong>Meaning</strong></p></td><td colspan="1" rowspan="1"><p><strong>Example</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p>* (asterisk)</p></td><td colspan="1" rowspan="1"><p>Select all possible values in a field</p></td><td colspan="1" rowspan="1"><p>Place * in the <strong>hour</strong> field to run the task every hour.</p></td></tr><tr><td colspan="1" rowspan="1"><p>, (comma)</p></td><td colspan="1" rowspan="1"><p>A comma is used to separate multiple values</p></td><td colspan="1" rowspan="1"><p>0,3,5 in the <strong>day of week</strong> field will make the task run on Sunday and Wednesday.</p></td></tr><tr><td colspan="1" rowspan="1"><p>– (hyphen)</p></td><td colspan="1" rowspan="1"><p>Used to set a range of values</p></td><td colspan="1" rowspan="1"><p>10-15 in the <strong>day of month</strong> field will run the task from the 10th to the 15th day of the month.</p></td></tr><tr><td colspan="1" rowspan="1"><p>/ (separator)</p></td><td colspan="1" rowspan="1"><p>A separator is used to divide values</p></td><td colspan="1" rowspan="1"><p>*/10 in the <strong>hour</strong> field will make the task run every 10 hours.</p></td></tr></tbody></table>

Hey there! I know it might seem a bit puzzling at first, so let's go through an example together to make it clearer:

```bash
# runs command at 5:30 every day , every month 
30 5 * * *  command
# runs command at 8:00 every day of month from 10th day to 20th day
0 8 10-20 * * command
# runs command at 7:30 in March 28,29,30 
30 7 28,29,30 3 * 
# runs command after every 10th hour in the month of July
0 */10 * 7 *
```

You can check out this amazing website where you can practice specifying cron entries like a pro! 🤩🎉 &gt; [https://crontab.guru](https://crontab.guru)

### 🔸I/O redirection:

Redirection is a feature in Linux such that when executing a command, you can change the standard input/output devices. The basic workflow of any Linux command is that it takes an input and gives an output.

The shell has three standard streams in I/O redirection:

* **standard input (stdin):** The stdin stream is numbered as stdin (0). The bash shell takes input from stdin. By default, the keyboard is used as input.
    
* **standard output (stdout):** The stdout stream is numbered as stdout (1). The bash shell sends output to stdout. Output goes to display.
    
* **standard error (stderr):** The stderr stream is numbered as stderr (2). The bash shell sends an error message to the stderr. Error message goes to display.
    

```bash
# sends standard output to file and rewrites it 
echo "hello world" > hello.txt
# sends standard output to file and and appends the text in file
echo "hello world" >> hello.txt
# sends error output to file 
ls non_existent_file > no_file_error.txt
# send error output to standard output 
ls non_existent_file 2>&1
```

When `>` is used with a file it rewrites the file with new content, but when `>>` is used new content is appended into the file.

### 🔸 pipe operator in Linux

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689785288664/b3a229b9-83a1-4952-be31-b010111bbf31.png align="center")

In Linux, the pipe operator enables two or more commands to be combined or executed simultaneously. This means the output of one command is used as input for the next one, and so on. The name "pipe" is quite fitting, as it refers to the concept of a process flow being channeled through a pipe from a source to a destination.

Here are various examples to help you better understand the concept:

```bash
# feed the input of grep command with the output of cat command 
$ cat /etc/passwd | grep localuser
localuser:×:1000:1000:Local User:/home/localuser/bin/bash

# check available ram with the help of free command
free -h | grep Swap | awk '{print $2}'
```

## 📍Conclusion:

In conclusion, these advanced shell scripting concepts significantly enhance your Linux skills by providing a deeper understanding of case statements, looping statements, sequence expressions, the seq command, cron jobs, I/O redirection, and the pipe operator. By mastering these concepts, you can efficiently automate tasks, and streamline your daily workflow.

Happy Learning