---
title: "🚀 Day - 1 of Bash scripting challenge ! 🚀 #TWSBashBlazeChallenge"
seoTitle: "Day - 1 of Bash scripting challenge ! 😎🚀 #TWSBashBlazeChallenge"
seoDescription: "Day 1 Bash Scripting: Master DevOps automation, covering fundamentals, shebang, comments, echo, variables, and wildcards"
datePublished: Tue Aug 01 2023 04:15:45 GMT+0000 (Coordinated Universal Time)
cuid: clkrsdnc8000409mcgr3p7aot
slug: day-1-of-bash-scripting-challenge-twsbashblazechallenge
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690863167100/0626b7c7-1409-4528-bc5b-dea1708789ef.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690863253744/0ede0187-f3a6-486f-a7ed-05a124c7a065.png
tags: linux, devops, learning-journey, bash-scripting, twsbashblazechallenge-trainwithshubham

---

## **📍 Introduction:**

Bash is a scripting language that is highly beneficial in DevOps, as it enables us to create scripts that assist in automating our daily workflow. Today, in this challenge, we will complete a series of tasks and create a Bash script that demonstrates fundamental concepts in Bash scripting. This will help us establish a solid foundation for writing more advanced scripts.

## ✔ Always start with the shebang!

If you're curious about what a shebang is, it's the very first line of every Bash script that informs the interpreter which shell should be used to execute your commands. It goes something like this `#!/bin/bash`.

## ✔ Now, let's move on to the tasks.

### 🔸 Task 1: **Comments**

Comments in a Bash script help us understand the script's purpose and functionality. In a Bash script, comments begin with the # symbol.

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 01-08-2023
# Description: #TWSBashBlazeChallenge Day - 1

# Task 1: Comments
# - In this task, we will use comments to explain the script.
```

### 🔸 Task 2: echo

The echo command is easy to understand, it helps print text on the screen. To use it, simply write the message after typing "echo", or use a pair of double quotes if you want to include a value from a variable in the message.

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 01-08-2023
# Description: printing a message on screen using echo command

echo "Today is Day 1 of #TWSBashBlazeChallenge an amazing bash scripting challenge"
```

### 🔸 Task 3: Variables

Variables in bash are like containers that allow us to store data and can be referenced by their name. Let's create a variable and assign a value to it.

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 01-08-2023
# Description: use variable to store values

# declaring and initializing variables
name = "Yashraj Jaiswal"
interests = "web dev | devops"
```

### 🔸 Task 4: Using variables

Now that we have declared some variables, let's utilize them to display a message on the screen using the echo command.

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 01-08-2023
# Description: use variables to print message on screen

# declaring and initializing variables
name = "Yashraj Jaiswal"
interests = "web dev and devops"

echo "Hello, my name is $name and I am interesed in $interests"
```

### 🔸 Task 5: Built-in variables

When working with bash it has some variables that are built into it and can help us access useful information regarding our system.

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 01-08-2023
# Description: use built-in variables from bash to print useful information

# print the host name
echo "Hostname: $HOSTNAME"

# print the current user
echo "Current user: $USER"

# print the current working directory
echo "Current directory: $PWD"
```

### 🔸 Task 6: Wildcard

Wildcards are characters that help define patterns for searching or matching text within string data in the Bash shell. They are also commonly used to create regular expressions.

Three mainly used wild cards are:

* Star or Asterisk (\*)
    
* Question mark (?)
    
* Square brackets (\[\])
    

Let's utilize these wildcards to assist us in our file searches.

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 01-08-2023
# Description: use wild cards to search for files

# using * wild card to search for files ending in .txt
ls -al *.txt

# using ? wild card to search for files names ending with a single unknown character
ls -al file?.txt

# using [] wild card to search for files that start with 'file' and have numbers 0-5
ls -al 'file[0-5]'.txt
```

## It's just the beginning: 😎

This is only Day 1 of the amazing Bash Blaze Challenge by #tws 😮, and it's already so exciting! We're going to keep going strong 💪 until Day 7, and by the end, we'll be absolute masters of Bash scripting! 🎉🚀 Let's keep learning and growing together!!