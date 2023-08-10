---
title: "🛠️ Fixing a broken restaurant ordering system in bash script📜.🍔😋"
seoTitle: "🛠️ Fixing a broken restaurant ordering system in bash script📜.🍔😋"
seoDescription: "🚀 Day 6 of Bash scripting challenge #TWSBashBlazeChallenge🔥🔥 Part-2 Fixing a broken restaurant ordering system"
datePublished: Sun Aug 06 2023 07:27:55 GMT+0000 (Coordinated Universal Time)
cuid: clkz4g0wm000509l52isfc5w3
slug: fixing-a-broken-restaurant-ordering-system-in-bash-script
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691306833409/2cdb4486-6896-46a9-910e-dbccaeab4c24.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691306849226/0ece8fc1-9ca2-429b-b3bd-3943a31ba23c.png
tags: linux, devops, 90daysofdevops, trainwithshubham, twsbashblazechallenge-trainwithshubham

---

## **📍** Introduction:

Hey there! So, we just cracked the [mystery bash script](https://yashraj-jaiswal.hashnode.dev/analyzing-a-mysterious-bash-script-part-1-of-day-6) challenge, and now we're diving into a fun new challenge. We'll be fixing a bash script designed for a restaurant ordering system. At first, it's not working, but with our awesome scripting skills, we'll get it up and running in no time!

## 🤔 This script seems to be broken and commented with a lot of **TODO**'s:🔧

```bash
#!/bin/bash

# Function to read and display the menu from menu.txt file
function display_menu() {
    echo "Welcome to the Restaurant!"
    echo "Menu:"
    # TODO: Read the menu from menu.txt and display item numbers and prices
    # Format: 1. Burger - ₹120
    #        2. Pizza - ₹250
    #        3. Salad - ₹180
    #        ...
}

# Function to calculate the total bill
function calculate_total_bill() {
    local total=0
    # TODO: Calculate the total bill based on the customer's order
    # The order information will be stored in an array "order"
    # The array format: order[<item_number>] = <quantity>
    # Prices are available in the same format as the menu display
    # Example: If the customer ordered 2 Burgers and 1 Salad, the array will be:
    #          order[1]=2, order[3]=1
    # The total bill should be the sum of (price * quantity) for each item in the order.
    # Store the calculated total in the "total" variable.
    echo "$total"
}

# Function to handle invalid user input
function handle_invalid_input() {
    echo "Invalid input! Please enter a valid item number and quantity."
}

# Main script
display_menu

# Ask for the customer's name
# TODO: Ask the customer for their name and store it in a variable "customer_name"

# Ask for the order
echo "Please enter the item number and quantity (e.g., 1 2 for two Burgers):"
read -a input_order

# Process the customer's order
declare -A order
for (( i=0; i<${#input_order[@]}; i+=2 )); do
    item_number="${input_order[i]}"
    quantity="${input_order[i+1]}"
    # TODO: Add the item number and quantity to the "order" array
done

# Calculate the total bill
total_bill=$(calculate_total_bill)

# Display the total bill with a personalized thank-you message
# TODO: Display a thank-you message to the customer along with the total bill
# The message format: "Thank you, <customer_name>! Your total bill is ₹<total_bill>."
```

## ✔ Overview of all the working functionality:

1. **populating the menu:**
    
    * The restaurant's menu is stored in a separate text file to allow easy editing without anyone interacting with the code logic this will make our script more modular.
        
    * The goal is to load the contents of the menu.txt file into a structured data format for manipulation.
        
    * To achieve this, we will use a function called `populate_menu`.
        
    * The `populate_menu` function takes the content of the menu.txt file as input.
        
    * Inside the function, the content is added to an associative array.
        
    * This approach enhances the manageability of menu data, allowing efficient interactions with the menu contents.
        
2. **displaying the menu:**
    
    * Now we need to display the menu to the user.
        
    * This is accomplished through the `display_menu` function.
        
    * Inside the function, a loop iterates through `menu_items` and `menu_item_value`.
        
    * During each iteration, the menu items and their corresponding values are presented to the user.
        
3. **take order:**
    
    * Now to take order from the user we create a function called `take_order`, this function manages the process of placing an order.
        
    * During this process, the user is presented with an individual menu item and prompted to enter the desired quantity for that item.
        
    * The function performs validation by checking if the user's input is a numeric value.
        
    * If the input is not a number, an error message is displayed, and the user is prompted again for input.
        
    * If the user presses enter without entering any value, the function proceeds to the next item.
        
    * When the user enters a valid number, the quantity is added to their order.
        
4. **calculate the total bill:**
    
    * To calculate the bill we create a `calculate_total_bill` function.
        
    * The function performs calculations based on the items and quantities in the user's order that is stored in the previously defined associative arrays.
        
5. **main function:**
    
    * The `main` function serves as the central point where all components of the ordering system are integrated and the ordering process is initiated.
        
    * The execution starts by calling the `display_menu` function to present the menu items and their values to the user.
        
    * Subsequently, the `take_order` function is called, allowing the user to input their desired order quantities.
        
    * Following that, the `calculate_total_bill` function is invoked to compute the total cost of the user's order.
        
    * Finally, a concluding message is displayed to provide the user with the total bill amount.
        
6. **putting it all together:**
    
    * Our restaurant's ordering system operations are coordinated after defining the `main` function.
        
    * The initial step involves populating an array with values from the `menu.txt` file. This is achieved by calling the `populate_menu` function.
        
    * After the array is populated, the `menu` function is called. This function integrates and executes all the functionalities of the restaurant ordering system, offering a comprehensive user experience.
        

## ✔ Final script:

After fixing the script and implementing all the above-mentioned functionalities, here's the final script.

```bash
#!/bin/bash
# This is a bash script that simulates a restaurant ordering system.

# Declare associative arrays to store menu item values, ordered quantities, and menu items.
declare -A menu_items
declare -A menu_item_value
declare -A item_quantity_ordered

# Function to read menu items and their values from a file and populate the associative arrays.
function populate_menu() {
    local menu_file="./menu.txt"
    local index=0
    while IFS=", " read -r menu_item menu_item_value; do
        menu_items[$index]=$menu_item
        menu_item_value[$menu_item]=$menu_item_value
        ((index++))
    done < "$menu_file"
}

# Function to display the menu items and their corresponding values.
function display_menu() {
    local index=1
    for key in "${menu_items[@]}"; do
        echo -e "$index. $key \t- ₹ ${menu_item_value[$key]}"
        ((index++))
    done
}

# Function to take the customer's order for various menu items.
function take_order() {
    local index=1
    echo "Menu items will appear one at a time. Enter the quantity when prompted."
    echo "If you don't require an item, just press enter, and we will move to the next item."
    
    # take input for every item in the menu
    for key in "${menu_items[@]}"; do
        # take input from the customer until a numeric value is added 
        while true; do
            read -p "$index. $key: " quantity
            # if input is empty move to next item
            if [[ -z "$quantity" ]]; then
                break
            # add to order only when input is a number    
            elif [[ $quantity =~ ^[0-9]+$ ]]; then 
                item_quantity_ordered["$key"]=$quantity
                break
            # for any input other than a number keep prompting the user for a numeric input
            else
                # Print an informative message to indicate the user that the input can only be a number.
                echo "Invalid input, enter quantity in number. Or press enter if item not required."
                continue
            fi
        done
        ((index++))
    done
}

# Function to calculate the total bill based on the ordered quantities and item values.
function calculate_total_bill() {
    local total=0
    for key in "${menu_items[@]}"; do
        total=$((total + menu_item_value[$key] * item_quantity_ordered[$key]))
    done
    echo $total
}

# Main function to execute the restaurant ordering process.
function main(){
    echo Welcome to the bash blaze restaurant 
    read -p "What's your name please : " customer_name
    echo "$customer_name, here is our amazing menu:"
    # Show the menu to the customer
    display_menu
    echo Ready to order!!
    # Take the customer's order
    take_order
    echo "Enjoy your meal, $customer_name..."
    echo 
    echo
    sleep 2
    echo "Thank you, $customer_name, for dining at our Bash Blaze restaurant."
    # Generate the bill and present it to the customer
    echo "Your total bill is: ₹$(calculate_total_bill)"
}

# Populate the menu items and values from the file.
populate_menu
# Call the main function to start the ordering process.
main
```

### ✔ Sample menu file:

```bash
Burger, 120
Pizza, 250
Salad, 180
Soda, 40
Pasta, 180
Sandwich, 150
Coke, 50
Fries, 100
Ice Cream, 120
```

Here's the final script and a sample menu file for you to enjoy! Run the command and have fun ordering from our "Bash Blaze Restaurant" 😊🍔🍕🥗🥤

### ✔ Output after running the fixed script:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691301923486/19f1d79e-010c-4bea-a815-e15320eb96d2.png align="center")

## **📍** Conclusion:

We did it! We nailed fixing the broken bash script for the restaurant ordering system! We implemented super important functionalities like populating the menu, displaying it, taking orders, and calculating the total bill! Now the ordering process is smoother than ever, and the user experience is fantastic! 🎉🍔🍕🥗