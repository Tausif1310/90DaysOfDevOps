---
title: "Shell Script  Task"
datePublished: Thu Feb 13 2025 17:28:22 GMT+0000 (Coordinated Universal Time)
cuid: cm73m5pcv000508jsemoa3cqk
slug: shell-script-task
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739467458583/c9d5f6bc-7764-4ebe-9fcc-e32c831c0d9e.jpeg
tags: linux, devops, shell-script, 90daysofdevops, tws

---

# 🐧 Shell Script to Create User Accounts with `-c` or `--create` Option 🛠️

Are you tired of manually creating user accounts on your Linux system? 🤔 Do you want a quick and easy way to automate user creation with a simple script? Look no further! In this blog, I’ll walk you through a **shell script** that allows you to create new user accounts with just one command. Let’s dive in! 🚀

## Week 3 Challenge 1: User Account Management

In this challenge, you will create a bash script that provides options for managing user accounts on the system. The script should allow users to perform various user account-related tasks based on command-line arguments.

* ### Part 1: Account Creation
    

1. Implement an option `-c` or `--create` that allows the script to create a new user account. The script should prompt the user to enter the new username and password.
    
2. Ensure that the script checks whether the username is available before creating the account. If the username already exists, display an appropriate message and exit gracefully.
    
3. After creating the account, display a success message with the newly created username.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739463428148/9ed68148-f1fe-42aa-a4b5-430c937a7465.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739463574474/c1e488b1-b608-42d8-b632-50950df717f4.png align="center")

## 💡 Key Features

* **User-Friendly Prompts**: The script guides the user step-by-step.
    
* **Username Availability Check**: Prevents duplicate usernames.
    
* **Secure Password Input**: Passwords are hidden during input.
    
* **Graceful Error Handling**: Displays clear error messages and exits gracefully.
    

---

## 🛑 Important Notes

* **Privileges Required**: The script uses `sudo` to run `useradd`, so you need root or sudo privileges for run command
    
* **Password Hashing**: The script uses `openssl passwd -1` for password hashing. For production environments, consider using more secure hashing methods. in realtime you canuse this method
    
* **Linux-Specific**: This script is designed for Linux systems. Adjustments may be needed for other Unix-like systems.
    

### Part 2: Account Deletion

1. /Implement an option `-d` or `--delete` that allows the script to delete an existing user account. The script should prompt the user to enter the username of the account to be deleted.
    
2. Ensure that the script checks whether the username exists before attempting to delete the account. If the username does not exist, display an appropriate message and exit gracefully.
    
3. After successfully deleting the account, display a confirmation message with the deleted username.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739464240907/2ecf7154-d103-4581-a33c-acfda3215e94.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739464287732/fc5aaf27-1b1d-438c-bb68-b762867820ca.png align="center")

### Part 3: Password Reset

1. Implement an option `-r` or `--reset` that allows the script to reset the password of an existing user account. The script should prompt the user to enter the username and the new password.
    
2. Ensure that the script checks whether the username exists before attempting to reset the password. If the username does not exist, display an appropriate message and exit gracefully.
    
3. After resetting the password, display a success message with the username and the updated password.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739464820539/34313a7a-82cf-4885-8d0f-51414a7e758f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739464852154/8fceb44f-444d-468b-830d-74615a78a801.png align="center")

### 💡 Key Features

* **User-Friendly Prompts**: The script guides the user step-by-step.
    
* **Username Existence Check**: Ensures the account exists before attempting to reset the password.
    
* **Secure Password Input**: Passwords are hidden during input.
    
* **Graceful Error Handling**: Displays clear error messages and exits gracefully.
    

---

### 🛑 Important Notes

* **Privileges Required**: The script uses `sudo` to run `chpasswd`, so you required root or sudo privileges.
    
* **Password Security**: Ensure that the new password follows your system's password policy.
    
* **Linux-Specific**: This script is designed for Linux systems. Adjustments may be needed for other Unix-like systems.
    

### Part 4: List User Accounts

1. Implement an option `-l` or `--list` that allows the script to list all user accounts on the system. The script should display the usernames and their corresponding user IDs (UID).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739465404039/899ffd71-074e-4d8a-bfea-13b4ce957208.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739465442712/04203998-3e66-4a72-801d-9b809d95745f.png align="center")

* ## Submission Instructions
    
    Create a bash script named `user_`[`management.sh`](http://management.sh) that implements the User Account Management as described in the challenge.
    
    Add comments in the script to explain the purpose and logic of each part.
    

user\_managemet script

```powershell
#!/bin/bash

# Function to create a new user
create_user() {
    read -p "Enter new username: " username

    if id "$username" &>/dev/null; then
        echo "Error: The username '$username' already exists. Please choose a different username."
        exit 1
    fi

    read -s -p "Enter new password: " password
    echo

    sudo useradd -m -p $(openssl passwd -1 "$password") "$username"

    if [ $? -eq 0 ]; then
        echo "Success: The user '$username' has been created."
    else
        echo "Error: Failed to create the user '$username'."
        exit 1
    fi
}

# Function to delete a user account
delete_user() {
    read -p "Enter the username to delete: " username

    if ! id "$username" &>/dev/null; then
        echo "Error: The username '$username' does not exist. Please check the username and try again."
        exit 1
    fi

    sudo userdel -r "$username"

    if [ $? -eq 0 ]; then
        echo "Success: The user '$username' has been deleted."
    else
        echo "Error: Failed to delete the user '$username'."
        exit 1
    fi
}

# Function to reset a user's password
reset_password() {
    read -p "Enter the username to reset password: " username

    if ! id "$username" &>/dev/null; then
        echo "Error: The username '$username' does not exist. Please check the username and try again."
        exit 1
    fi

    read -s -p "Enter the new password: " new_password
    echo

    echo "$username:$new_password" | sudo chpasswd

    if [ $? -eq 0 ]; then
        echo "Success: The password for user '$username' has been reset."
    else
        echo "Error: Failed to reset the password for user '$username'."
        exit 1
    fi
}

# Function to list all user accounts
list_users() {
    echo "Listing all user accounts on the system:"
    echo "--------------------------------------"
    getent passwd | awk -F: '{print "Username:", $1, "| UID:", $3}'
}

# Main script logic
if [[ $1 == "-c" || $1 == "--create" ]]; then
    create_user
elif [[ $1 == "-d" || $1 == "--delete" ]]; then
    delete_user
elif [[ $1 == "-r" || $1 == "--reset" ]]; then
    reset_password
elif [[ $1 == "-l" || $1 == "--list" ]]; then
    list_users
else
    echo "Usage: $0 -c|--create | -d|--delete | -r|--reset | -l|--list"
    exit 1
fi
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1739467207913/2e8a18fc-961d-4de0-8868-85d8f2b719af.png align="center")