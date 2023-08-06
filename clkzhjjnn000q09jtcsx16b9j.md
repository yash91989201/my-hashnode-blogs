---
title: "🔧 Repairing a recursive file search function 🔍⚙️"
seoTitle: "🔧 Repairing a recursive file search function 🔍⚙️"
seoDescription: "🚀 Day 6 of Bash scripting challenge #TWSBashBlazeChallenge🔥🔥 Part-3 Fixing a recursive file search function"
datePublished: Sun Aug 06 2023 13:34:34 GMT+0000 (Coordinated Universal Time)
cuid: clkzhjjnn000q09jtcsx16b9j
slug: repairing-a-recursive-file-search-function
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691328803202/cab9e6eb-e6e8-4f9d-b086-78fac30f0af7.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691328847784/4ed07c04-9820-41a6-9de4-efeba3530b10.png
tags: linux, devops, 90daysofdevops, trainwithshubham, twsbashblazechallenge-trainwithshubham

---

## **📍** Introduction:

In the third and final part of Day 6 in the #TWSBashBlaze challenge, we will be repairing a function designed to search for a file in a directory recursively. If the file is not found, the function will continue to search within its subdirectories, also recursively.

## ✔ Overview:

1. **Validating User Input:**
    
    * The process starts by conducting checks on the user's input.
        
    * If the user hasn't provided two arguments, the system prints usage information to guide proper usage.
        
    * Additionally, if the specified search directory given by the user does not exist, an error message is displayed, and the program exits.
        
2. `recursive_file_search` **function:**
    
    * The `recursive_file_search` function encapsulates the required logic to fulfill the task at hand.
        
    * Within this function, a `current_dir` variable is established to hold the name of the current directory being examined.
        
    * The function involves iterating through the contents of the current directory.
        
    * If a file within the current directory is a directory, the `recursive_file_search` function is called again. This recursive call initiates the search within the subdirectory.
        
    * Upon locating the desired file, a success message is displayed, followed by the absolute path of the found file.
        
3. **printing the absolute path of the file:**
    
    * When the target file is successfully located, a success message is printed.
        
    * This success message is followed by displaying the absolute path of the found file.
        
    * Also, if the file is not found during the search, an appropriate error message is displayed to indicate that the file could not be located.
        

## ✔ Final Script:

```bash
#!/bin/bash
# Author: Yashraj Jaiswal
# Date: 05/08/2023
# Description: #TWSBashBlazeChallenge Day-6
# Task part -3 : fix the recursive search script

if [ $# -ne 2 ]; then
    echo "Usage : ./recursive_search.sh <directory> <target_file>"
    exit 1
fi

search_dir="$1"
target_file="$2"

# Function to perform recursive search for the target file
function recursive_file_search {
    local current_dir="$1"
    
    # Loop through the contents of the current directory
    for file in "$current_dir"/*; do
        if [ -d "$file" ]; then
            # If the current item is a directory, call the recursive_file_search function to check within the sub directory
            recursive_file_search "$file"
            elif [ -f "$file" ] && [[ "$(basename "$file")" == "$target_file" ]]; then
            # If the current item is a file and its name matches the target file, print a success message
            # then print the absolute path of the file
            echo "File found!!!"
            echo "Absolute path of $target_file - $file"
            exit 0
        fi
    done
}

# Check if the provided directory exists
if [ ! -d "$search_dir" ]; then
    echo "Error: Directory '$search_dir' not found."
    exit 1
fi

# Start the recursive search by calling the recursive_file_search function with the provided search directory
recursive_file_search "$search_dir"

# If the loop completes without finding the target file, display a "File not found" message and exit with an error
echo "File not found: $target_file"
exit 1
```

## **📍** Conclusion:

This is amazing! We fixed the recursive search function, and now we can also use this script to search for files whenever we want. This was the last part of Day 6 challenge in the #TWSBashBlaze challenge. All the parts up until this one were challenging and fun to solve. Let's wait and see what challenges Day 7 brings up.