# Setup Ubuntu 20.04 server

## User management

### Step 1 - Loggin in as root

`ssh root@ip_address`

**NOTE**: Avoid using *root* account as much as possible

### Step 2 - Creating a New user

`adduser username`

Answe the questions that follow about the user

### Step 3 - Granting administrative Privileges

add user to the *sudo* group

`usermod -aG sudo username`

## Firewall Setup

### Step 1 - Basic setup

Ubuntu 20.04 servers can use the **UFW firewall** to make sure only connections to certain services are allowed.

`ufw app list` - shows available applications 

**NOTE**: we need to allow SSh connections to login using SSH

`ufw allow OpenSSH`

`ufw enable` - enable firewall

`ufw status` - firewall status

## External access for regular user

### Root account uses SSH key authentication

If you logged in to your root account using SSH keys, then password authentication is disabled for SSH. You will need to add a copy of your local public key to the new user’s ~/.ssh/authorized_keys file to log in successfully.

Since your public key is already in the root account’s ~/.ssh/authorized_keys file on the server, we can copy that file and directory structure to our new user account in our existing session.

The simplest way to copy the files with the correct ownership and permissions is with the rsync command. This will copy the root user’s .ssh directory, preserve the permissions, and modify the file owners, all in a single command. Make sure to change the highlighted portions of the command below to match your regular user’s name:

`rsync --archive --chown=sammy:username ~/.ssh /home/username`
