---
title: "Day - 2 of Bash scripting challenge !  #TWSBashBlazeChallenge 🔥🔥"
seoTitle: "Day - 2 of Bash scripting challenge !  #TWSBashBlazeChallenge 🔥🔥"
seoDescription: "Day - 2 of Bash scripting challenge !  #TWSBashBlazeChallenge 🔥🔥"
datePublished: Wed Aug 02 2023 04:16:25 GMT+0000 (Coordinated Universal Time)
cuid: clkt7ucoj000b0al8bjsz0u4l
slug: day-2-of-bash-scripting-challenge-twsbashblazechallenge
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690949675246/10ed5bda-3cce-4385-8db2-56f51a692d55.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690949740207/2e1ce8b4-4750-4892-94af-a02ac7643ca0.png
tags: linux, bash-scripting, 90daysofdevops, trainwithshubham, twsbashblazechallenge-trainwithshubham

---

## 📍 Moving on to day 2:

It's Day 2 🎉 of the #TWSBashBlazeChallenge, and we've got two amazing tasks lined up for today! 🤩 First up, we have file and directory exploration 🕵️‍♀️, and then we'll back up our directories like pros!! Let's get started! 🚀

## ✔ Task 1: File and directory exploration 📂🕵️‍♀️

For the first task, our script needs to display a welcome message on the screen, followed by the contents of the current directory along with their sizes in a human-readable format. Let's take a look at the solution script to address the given problem statement.

```bash
#!/bin/bash
#Author: Yashraj Jaiswal
# Date: 02/08/2023
# Description: #TWSBashBlazeChallenge Day-2
# Task 1: Interactive File and Directory Explorer

# print a welcome message for the user
echo Welcome to the Interactive File and Directory Explorer!

# Format and display files and directories 
# with their size in human readable format
echo "Files and Directories in current path - $PWD"
ls -lh | sed 1d | awk '{print "- ",$NF,"\t","(",$5,")"}'

# Infinite loop to continiously take user input
while true;
do
        # prompt user to enter a text
        echo -n "Enter a line of text (Press Enter without text to exit)"
        read input
        # use -z option to test for empty string
        if [[ -z $input ]];
        then
                echo Exiting the interactive explorer. Goodbye!
                exit
        else
                # bash built-in string length
                input_length=${#input}
                # print the character count on screen
                echo "Character count $input_length"
        fi
done
```

Upon executing the script we will get the following output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690914855596/51aa0fd0-4262-49c7-a104-0dbcd7db0cf8.png align="center")

## ✔ Task 2: Directory backup with rotation 🔄

For the second task, we need to create a Bash script that accepts a directory path as a command-line argument and performs a backup of the directory. The script should generate timestamped backup folders and copy all the files from the specified directory into the backup folder.

Additionally, the script should implement a rotation mechanism to maintain only the last three backups. This means that if there are more than three backup folders, the oldest backup folders should be removed to ensure only the most recent backups are retained.

Let's take a look at the solution script to address the given problem statement.

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 01/08/2023
# Description: TWSBashBlazeChallenge Day-2
# Task 2: Directory Backup with Rotation

# Validate input parameter for the directory to backup
if [ "$#" -ne 1 ]; 
then
    echo "Usage: $0 <path_to_directory>"
    echo "Hint : Enter the full path to the directory to backup"
    exit 1
fi

# variable that we will need later 
path_to_dir="$1"
backup_dir="/var/backups"
max_backup_files=3

# Get the number of existing backup files in the backup directory
total_backup_files=$(find "$backup_dir" -type f -name "*.tgz" | wc -l)
echo
echo "Total backup files: $total_backup_files"

# Check if more than the allowed number of backup files exist
if (( total_backup_files >= max_backup_files )); 
then
        echo
        echo "More than $max_backup_files backup files detected"
        # Sort the backup files by modification time and delete the oldest one
        oldest_file=$(find "$backup_dir" -type f -name "*.tgz" | sort -r | tail -n 1)
        echo "Deleting the oldest backup file - $oldest_file"
        sudo rm -f "$oldest_file"
fi

# Create a new tar file with timestamp in the filename
backup_file="backup_$(date +%d_%m_%Y_%H_%M_%S).tgz"
sudo tar -cvzf "$backup_dir/$backup_file" "$path_to_dir" > /dev/null 2>&1

# Check if the tar command executed successfully
if [[ $? -eq 0 ]]; 
then
        echo
        echo "Backup created successfully"
        echo "List of backups created in the past 3 days:"
        sudo ls -lh "$backup_dir"/*.tgz |  awk '{print "-",$NF, "\t(", $5, ")"}'
else
        echo "Unable to create backup"
fi
echo
```

Here is the output when we run the above script:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690949255682/9e9fdcba-4d4c-4339-9fd3-ff02bbf7a34f.png align="center")

## 📍 Conclusion:

Day 2 of the #TWSBashBlazeChallenge is all about diving into the thrilling world of files and folders, and mastering the art of folder backups with rotation! 🎉

Get ready to level up your skills by learning how to perform backups like a pro, take input from command line arguments, and powerfully filter the 'ls' command to achieve the results you' can efficiently use to your advantage! 💪🚀