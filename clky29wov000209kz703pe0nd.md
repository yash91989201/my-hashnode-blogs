---
title: "🗂️ A beginner's guide to log analysis 💡 using bash scripts. 🧾🔥🔥"
seoTitle: "🗂️ A beginner's guide to log analysis 💡 using bash scripts. 🧾🔥🔥"
datePublished: Sat Aug 05 2023 13:39:24 GMT+0000 (Coordinated Universal Time)
cuid: clky29wov000209kz703pe0nd
slug: a-beginners-guide-to-log-analysis-using-bash-scripts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691242625169/74fb0b92-f890-4a07-89f7-e34de8734944.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691242724177/9a6a6f72-18d9-48fd-9ed1-4aff5fee3471.png
tags: linux, bash-script, 90daysofdevops, trainwithshubham, bashblaze-7-days-of-bash-scripting-challenge

---

## **📍** Introduction:

When working with Linux systems, log files are constantly generated, and analyzing them to draw meaningful conclusions can be quite a hassle! But don't worry, we've got the perfect solution! We can create an awesome bash script that'll analyze those log files and magically turn them into a super handy summary! How cool is that?!

In this blog, we are going to write a handy bash script to generate a summary out of a log file.

## ✔ Script Overview: 📃👀

Let's look at some points that we will be covering in our script:

1. **Input**: The script accepts the log file's path as a command-line argument.
    
2. **Error Count**: The script analyzes the log file and tallies the number of error messages. Error messages can be identified by keywords such as "ERROR" or "Failed," and the script displays the total error count.
    
3. **Critical Events**: The script searches for lines containing the keyword "CRITICAL" and prints those lines along with the line number.
    
4. **Top Error Messages**: It identifies the top 5 most common error messages and displays them along with their occurrence count.
    
5. **Summary Report**: he script generates a summary report in a separate text file, which includes the date of analysis, log file name, total lines processed, total error count, top 5 error messages, and a list of critical events with their corresponding line numbers.
    
6. **Organizing the report:** Output the summary report in a separate file labeled with the current date and move it to the /var/log directory, where most logs are found in Linux.
    

## ✔Implementing the script: 💡

```bash
#!/bin/bash
#Author: Yashraj Jaiswal
# Date: 05/08/2023
# Description: #TWSBashBlazeChallenge Day-5
# Task : create a log analyzer script

function error_count(){
    egrep -i -c "ERROR|faliure" $1
}

function critical_events(){
    filename="your_file.txt"
    pattern="CRITICAL"
    line_number=1
    while IFS= read -r line; do
        if [[ $line == *"$pattern"* ]]; then
            echo "Line $line_number: $line"
        fi
        ((line_number++))
    done < "$1"
}

function top5_error_message(){
    egrep -i "ERROR|faliure" "$1" | sort | rev | cut -d ' ' -f 3- | rev | uniq -c | sort -r  | head -5
}

function generate_summary(){
    echo "Date of analysis      : $(date +"%D")"
    echo "Log file name         : $1"
    echo "Total line processed  : $(wc -l $1 | awk '{print $1}')"
    echo "Total error count     : $(error_count $1)"
    echo
    echo
    echo "Top 5 error messages:"
    echo
    top5_error_message "$1"
    echo
    echo
    echo "List of critical events with line number : "
    echo
    critical_events "$1"
}

function main(){
    # check if the user has passed any file in command line
    if (( $# == 0 )); then
        echo "Info  : this script analyzes a log file and creates a summary out of it."
        echo "Usage : $0 path-to-file."
        exit 1
    fi
    # check if the given file is empty or not.
    if [ ! -s "$1" ]; then
        echo "$1 file is empty"
        exit 1
    fi
    local log_summary_file="log_summary_$(date +"%Y_%m_%d").txt"
    touch "$log_summary_file"
    generate_summary "$1" > "$log_summary_file"
    sudo mv "./$log_summary_file" /var/log
    echo "Summary report generated: /var/log/$log_summary_file"
}

main "$1"
```

Upon executing the above script with a sample log file, we receive the following output in a text file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691242941856/a1579946-7330-4ce3-937c-db28a3a094da.png align="center")

## **📍** Conclusion:

Oh my gosh! We've just created this incredible bash script that's going to be a game-changer for us every single day! Now we have this super convenient bash script at our fingertips, ready to run and instantly provide us with a summary of our log report! Feel free to customize this fantastic script to perfectly suit your needs! Make it your own and unleash its full potential!