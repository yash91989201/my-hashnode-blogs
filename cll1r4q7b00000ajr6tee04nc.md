---
title: "⚙️ Deploy Docker Applications Remotely through Bash Scripts.🐳📜"
seoTitle: "⚙️ Deploy Docker Applications Remotely through Bash Scripts.🐳📜"
seoDescription: "🚀 Day 7 of Bash scripting challenge #TWSBashBlazeChallenge🔥🔥"
datePublished: Tue Aug 08 2023 03:38:31 GMT+0000 (Coordinated Universal Time)
cuid: cll1r4q7b00000ajr6tee04nc
slug: deploy-docker-applications-remotely-through-bash-scripts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691465837271/f3441f50-9e3a-44b5-97e1-8b11f0f75aea.gif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691465891022/e1b61058-d8cd-4dd2-b29a-5696053adbe9.gif
tags: docker, devops, bash-script, 90daysofdevops, twsbashblazechallenge-trainwithshubham

---

## **📍** Introduction:

Today is the FINAL day of the epic #TWSBashBlazeChallenge, and we're going all out by deploying a Docker project on remote servers using bash script! 🎉 Get ready to write a series of thrilling bash scripts that will guide us step by step toward successfully deploying our project! 🚀 Let's do this! 💪

## 🛠️ Prerequisites.

Before we dive in, make sure you have the following prerequisites in place:

1. public key to authenticate to the remote clients.
    
2. client list file, where all the client data is stored in the following format:
    
    `client_name, client_ip`
    
3. project file that you want to deploy which also contains the docker-compose file to deploy your application.
    

I have stored the client IP list in a separate file, allowing us to modify client data without altering our code.

Here is a sample client ip list file:

```bash
client1, 54.26.123.68
client2, 44.58.12.125
client3, 101.26.23.50
```

## ✔ Script 1: remote-execute.sh 📜

In this bash script, we will remotely execute commands on our remote machine to help us install the packages required to run our application. First, we will check if a package exists; if not, we will attempt to install it.

1. **validate user input:** We use the `validate_cmd_arg_input` to verify the input given by the user so that all our functions run smoothly without any issues.
    
2. **populate client data:** To utilize the client data from a separate file, we load the file contents into an array with the help of the `populate_client_list function`. This allows us to effortlessly loop through the clients and execute our tasks.
    
3. **executing command remotely:** We extract the SSH call into a separate function, allowing us to avoid specifying the options and key file for SSH each time. Instead, we can simply call the function with the command to execute.
    
4. install required packages: The install\_packages function installs docker and docker-compose on remote clients.
    

Finally, we assemble all our functions into one place and execute them sequentially in the main function to perform all our tasks.

```bash
#!/bin/bash
declare -A client_name_list
declare -A client_ip_list

function validate_cmd_arg_input(){
    echo
    echo "Step 1. Validating $1 file."
    # check if user has provided a file of clients to read from
    if [ $# -eq 0 ]; then
        # print usage information
        echo "Info  : This script prepares remote clients for remote connection throught the main server"
        echo "Usage : $0 /path/to/client_ip_list file"
        exit 1
    fi
    # check if the client list file provided by the user exists or not
    if [ ! -e "$1" ]; then
        echo "> The client ip list file provided does not exists."
        exit 1
    fi
    # check if the client list file is empty or not
    if [ ! -s "$1" ]; then
        echo "> The client ip list file provided is empty , please check and execute again"
        exit 1
    fi
    
    echo "> File validation successful."
}


function populate_client_list() {
    echo
    echo "Step 2. Load client list data from $1 file in the script."
    
    local index=1
    while IFS=', ' read -r name ip || [[ -n "$name" ]]; do
        if [[ -n "$name" ]]; then
            echo "Read: name='$name', ip='$ip'"
            client_name_list[$index]=$name
            client_ip_list["$name"]=$ip
            ((index++))
        fi
    done < "$1"
    
    echo "> Done."
}

function connect_and_execute(){
    ssh -o StrictHostKeyChecking=no -i ./ec2key "ubuntu@$1" "$2"
}

function install_packages(){
    echo "Step 3. Installing packages on all clients."
    
    for client_name in "${client_name_list[@]}";do
        local client_ip="${client_ip_list[$client_name]}"
        echo
        echo "Checking for docker on $client_ip"
        connect_and_execute "$client_ip" "which docker > /dev/null 2>&1"
        docker_installed=$?
        
        if [ $docker_installed -eq 0 ];then
            echo "Docker is already installed."
            echo
        else
            echo
            echo "Docker doesnot exists on $client_ip"
            echo "Installing now..."
            connect_and_execute "$client_ip" "sudo apt-get update && sudo apt install docker.io -y > /dev/null 2>&1"
            if [ $? -eq 0 ];then
                echo "Docker successfully installed on $client_ip"
            else
                echo "Unable to install docker."
            fi
        fi
        
        echo "Installing docker compose on $client_ip"
        connect_and_execute "$client_ip" "sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose > /dev/null 2>&1"
        
    done
}

function main(){
    # validate user input
    validate_cmd_arg_input "$1"
    sleep 1
    # populate client list data from the given flile
    populate_client_list "$1"
    sleep 1
    # if ssh key doesnot exists create it
    install_packages
}

main "$1"
```

## ✔ Step 2: secure-transfer.sh 📜

In this bash script, we will transfer our project files to the target hosts where we will be running our project.

1. **transfer the files:** after the input is validated and client data is loaded into the script we loop through all our clients and transfer our project file
    

```bash
#!/bin/bash
declare -A client_name_list
declare -A client_ip_list

function validate_cmd_arg_input(){
    echo "Step 1. Validating given files."
    
    for file in "$@"; do
        if [ ! -e "$file" ];then
            echo "$file doesnot exists."
            exit 1
        fi
        if [ ! -s "$file" ]; then
            echo "$file is empty."
            exit 1
        fi
    done
    echo "> File validation successful."
}

function populate_client_list() {
    echo
    echo "Step 2. Load client list data from $1 file into the script."
    
    local index=1
    while IFS=', ' read -r name ip || [[ -n "$name" ]]; do
        if [[ -n "$name" ]]; then
            echo "Read: name='$name', ip='$ip'"
            client_name_list[$index]=$name
            client_ip_list["$name"]=$ip
            ((index++))
        fi
    done < "$1"
    
    echo "> Done."
}

function connect_and_execute(){
    ssh -o StrictHostKeyChecking=no -i ./ec2key "ubuntu@$1" "$2"
}

function transfer_file(){
    for client_name in "${client_name_list[@]}";do
        local client_ip="${client_ip_list[$client_name]}"
        echo "Transferring project file to $client_ip"
        scp -o StrictHostKeyChecking=no -i "$1" -r node_docker "ubuntu@$client_ip:/home/ubuntu" > /dev/null 2>&1
    done
}

function main(){
    if [ $# -ne 2 ];then
        echo "Usage: ./secure_transfer.sh client_list_file clint_auth_key"
    else
        validate_cmd_arg_input "$@"
        populate_client_list "$1"
        transfer_file "$2"
    fi
}
main "$1" "$2"
```

## ✔ Script 3: deploy-app.sh 📜

Now that our project files have been sent to the target clients, we simply need to execute a command to deploy our app.

The `deploy_app` function loops through all the clients and executes a command to run our application on the clients using the ssh command.

```bash
#!/bin/bash
function validate_cmd_arg_input(){
    echo "Step 1. Validating given files."
    
    for file in "$@"; do
        if [ ! -e "$file" ];then
            echo "$file doesnot exists."
            exit 1
        fi
        if [ ! -s "$file" ]; then
            echo "$file is empty."
            exit 1
        fi
    done
    echo "> File validation successful."
}

function populate_client_list() {
    echo
    echo "Step 2. Load client list data from $1 file into the script."
    
    local index=1
    while IFS=', ' read -r name ip || [[ -n "$name" ]]; do
        if [[ -n "$name" ]]; then
            echo "Read: name='$name', ip='$ip'"
            client_name_list[$index]=$name
            client_ip_list["$name"]=$ip
            ((index++))
        fi
    done < "$1"
    
    echo "> Done."
}

function connect_and_execute(){
    ssh -o StrictHostKeyChecking=no -i ./ec2key "ubuntu@$1" "$2"
}

function deploy_app(){
    for client_name in "${client_name_list[@]}";do
        local client_ip="${client_ip_list[$client_name]}"
        echo "Deploying app on $client_ip"
        connect_and_execute "$client_ip" "cd node_docker && sudo docker-compose -f docker-compose.yaml -f docker-compose.prod.yaml up -d"
        echo
    done
}

function main(){
    if [ $# -ne 2 ];then
        echo "Usage: ./secure_transfer.sh client_list_file clint_auth_key"
    else
        validate_cmd_arg_input $@
        populate_client_list "$1"
        deploy_app
    fi
}
main "$1" "$2"
```

## ✔ Executing our scripts: 🔄⚙️

Execute the scripts in the specified order to simultaneously deploy your app on multiple clients. Additionally, ensure you have the required prerequisites to guarantee a smooth project execution.

After executing the scripts in proper order, we receive the following output, and our project is successfully deployed.🎉🥳

1. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691463190321/5ad7737b-3a43-4d52-9188-97035458aa01.png align="center")
    
2. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691463219595/d61add89-6764-4bb4-8848-b71d8cd963a4.png align="center")
    
3. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691463241516/18d3d350-4d95-4d37-b97e-370df8ad74e0.png align="center")
    
4. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691463264385/390b6c77-9acd-4510-ac0b-a1369ffcaf2e.png align="center")
    

And voila our project is running on different clients.

## **📍** Conclusion:

Woohoo! We've reached the grand finale of the #TWSBashBlazeChallenge, but hold on, this isn't the end of our thrilling bash journey! We'll be crafting more bash scripts in the future because, in the world of DevOps, we're always on the lookout for ways to automate our workflows. And guess what? From our exhilarating challenge days, we've discovered that bash is the ultimate tool for the job! 🎉🚀