---
title: "🔎 Monitoring system metrics and processes with a bash script. 🧾"
seoTitle: "🚀 Day 4 of Bash scripting challenge 
#TWSBashBlazeChallenge🔥🔥"
datePublished: Fri Aug 04 2023 15:42:50 GMT+0000 (Coordinated Universal Time)
cuid: clkwr8shd00070amoeswa2hoc
slug: monitoring-system-metrics-and-processes-with-a-bash-script
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691163621080/623a7245-284e-47cf-a0d3-b38f21a5a2ea.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691163738805/b84d0f98-4e30-4038-8fd3-b7416dc40303.png
tags: linux, devops, bash-script, 90daysofdevops, twsbashblazechallenge-trainwithshubham

---

## **📍** Introduction:

Welcome to Day 4 of our amazing Bash Scripting Challenge! Today, we're going to craft some super user-friendly scripts to keep an eye on system metrics and processes like a pro! Get ready to dive into a world of amazing functionalities, where we'll be showcasing CPU usage, memory usage, and available disk space!

But wait, there's more! We'll also be monitoring specific processes and giving users the power to restart them if they've stopped working! Let's get this party started!

## ✔ Why monitoring is important? 🤔

Monitoring finds problems early and helps you use resources better. It makes sure important parts work well. By monitoring services, you can ensure that critical components are up and running as expected.

## ✔ Part 1: Monitoring processes .📈

In this part, we will be creating a script that performs the following tasks:

1. Take a process name from the user as a command line argument.
    
2. Verify whether the service exists or not. If the service exists, determine if the process for that service is active or inactive.
    
3. If the process is active, display a message indicating that the process is running properly.
    
4. If, by any chance, the process is not running, attempt to restart it three times.
    
5. If the restart attempt is successful, display a success message; otherwise, print an error message.
    

Let's see how can we implement the above functionalities in a bash script.

```bash
#!/bin/bash
#Author: Yashraj Jaiswal
# Date: 03/08/2023
# Description: #TWSBashBlazeChallenge Day-4
# Task - part - 1 : Monitoring system process
# script start
# Define the name of the process you want to monitor
PROCESS_NAME="$1"
# Maximum number of restart attempts
MAX_RESTART_ATTEMPTS=3

# function to check if the given service exists or not
check_service_exists(){
    systemctl list-unit-files -q -all "$PROCESS_NAME.service"  > /dev/null 2>&1
}

# Function to check if the process is running
is_process_active() {
    local process_status=$(systemctl is-active $PROCESS_NAME 2> /dev/null)
    if [[ "$process_status" == "active" ]]; then
        exit 0
    else
        exit 1
    fi
}
# Function to restart the process
restart_process() {
    echo
    echo "Process '$PROCESS_NAME' is not running. Attempting to restart..."
    # Loop to check and restart the process
    for ((attempt=1; attempt<=$MAX_RESTART_ATTEMPTS; attempt++)); do
        if $(is_process_active); then
            echo "Process '$PROCESS_NAME' is running properly now."
            break
        else
            if [ $attempt -lt $MAX_RESTART_ATTEMPTS ]; then
                sudo systemctl restart $PROCESS_NAME
                sleep 2
            else
                echo "Maximum restart attempts reached. Please check the process '$PROCESS_NAME' manually."
                exit 1
            fi
        fi
    done
    echo
}

main(){
    echo
    # check if the services exists for the given process name
    check_service_exists
    if [ $? -eq 1 ];
    then
        echo "Service for process '$PROCESS_NAME' doesnot exists."
    else
        if $(is_process_active); then
            echo "Process '$PROCESS_NAME' is running properly."
        else
            restart_process
        fi
    fi
    echo
}

main
```

### 🔸 Let's see the working of the above script.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691162036843/3617ca68-3ce6-4144-b5da-11520a07fd9f.png align="center")

## ✔ Part 2: Monitoring metrics and specific processes.📋

In this part, we will create a script to perform the following tasks:

1. **Interactive menu:** Show an interactive menu that lists all the options our bash script has to offer.
    
2. **View system metrics:** Display system metrics information like CPU usage, memory usage, and disk space.
    
3. **Monitor Specific processes:** Enable the user to input a process name and display its status. If the process is inactive, present the user with the option to restart it.
    
4. **Exit the script**
    

Let's see how can we implement the above functionalities in a bash script.

```bash
#!/bin/bash
#Author: Yashraj Jaiswal
# Date: 03/08/2023
# Description: #TWSBashBlazeChallenge Day-4
# Task - part - 2 : Monitoring system metrics
# display metrics and monitor spcific process

check_service_exists(){
    systemctl list-unit-files -q -all "$1.service"  > /dev/null 2>&1
}

is_process_active() {
    local process_status=$(systemctl is-active "$1" 2> /dev/null)
    if [[ "$process_status" == "active" ]]; then
        exit 0
    else
        exit 1
    fi
}

# Function to restart the process
restart_process() {
    echo "Attempting to start process: $1"
    sudo systemctl restart $1
    if $(is_process_active "$1"); then
        echo "Process '$1' is running properly now."
    else
        echo "Unable to start $1 process."
    fi
    echo
}

display_system_metrics(){
    local continue_script=1
    until [[ $continue_script -eq 0 ]]
    do
        echo "----- System metrics -----"
        local cpu_usage=$(top -bn1 | grep '%Cpu' | awk '{print $2 + $4}')
        local mem_usage=$(free | awk '/Mem/{print $3/$2 * 100.0}')
        local disk_usage=$(df -h | awk '/\/dev\/root/{print $5}')
        echo "CPU Usage     : $cpu_usage%"
        echo "Memory Usage  : $mem_usage%"
        echo "Disk Space    : $disk_usage"
        echo "----- System metrics -----"
        echo "1. Print metrics again | 2. Go to main menu"
        read -p "Enter your choice: " choice
        
        if [[ $choice -eq 1 ]]; then
            continue_script=1
        else
            continue_script=0
        fi
    done
}

monitor_service(){
    echo
    echo "---------- Monitor a specific service ----------"
    read -p "Enter the name of the service you want to monitor : " service_name
    check_service_exists "$service_name"
    if [ $? -eq 1 ];
    then
        echo "Service for process - $service_name doesnot exists."
    else
        if $(is_process_active "$service_name"); then
            echo "$service_name is running."
        else
            echo "$service_name process is not running"
            read -p "Do you want to start $service_name (y/n) " choice
            if [ "$choice" == "y" ]; then
                restart_process "$service_name"
            fi
        fi
    fi
}

main() {
    local continue_script=0
    while [[ $continue_script -eq 0 ]]
    do
        echo
        echo "---------- Monitoring metrics script ----------"
        echo "1. View system metrics."
        echo "2. Monitor a specific service."
        echo "3. Exit"
        echo "---------- Monitoring metrics script ----------"
        echo
        read -p "Enter your choice: " choice
        case $choice in
            1) display_system_metrics;;
            2) monitor_service;;
            3) continue_script=1 ;;
            *) continue_script=1 ;;
        esac
    done
}

main
```

### 🔸 Let's see the working of the above script.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691162112992/861db14e-2bfe-49d8-a06d-c2392057824c.png align="center")

### **📍** Don't just stop here. 🔥🔥

The two scripts above serve an excellent purpose in addressing a problem when we need to view system metrics and manage processes. Feel free to add more functionality to these scripts to tailor them to your daily needs.

Keep an eye out for even more thrilling bash scripting challenges coming your way!! 🎉🚀