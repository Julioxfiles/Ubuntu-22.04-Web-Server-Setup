# Ubuntu-22.04-Web-Server-Setup
Describes the linux commands needed to set up a web server on ubuntu 22.04
We start from the idea that you already have an ssh file private key to connect to the ubuntu server where you will carry out the installation.
 
## Initial Server Setup with Ubuntu 22.04
Taken from: https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04

### Step 1 — Using your_ssh_file (private key) to log in as root on your ubuntu server.
$ ssh root@your_server_ip -i your_ssh_file -p your_port

### Step 2 — Creating a new user.

$ adduser your_new_user

Example: $ adduser julio // Add an ubuntu user. This can be your name or just "user" or "admin" or "ubuntu" or any other.

### Step 3 — Granting administrative privileges.

usermod -aG sudo your_new_user

Example: $ usermod -aG sudo julio

Note: You can now type sudo before commands to run them with superuser privileges when logged in as your regular user.

### Step 4 — Setting Up a Firewall
$ ufw app list // examine the list of installed UFW profiles.

$ ufw allow OpenSSH  //  Allows SSH connections.

$ ufw allow 22/tcp // We will use 22 as port to connect by ssh. The default port is 22.

$ sudo ufw allow http // This is the same as "sudo ufw allow 80/tcp"

$ sudo ufw allow https // This is the same as "sudo ufw allow 443/tcp"

$ ufw enable // Enable the firewall

$ ufw status // See that SSH connections are still allowed

### Step 5 — Enabling external access for your regular user on your ubuntu server.

$ rsync --archive --chown=sammy:sammy ~/.ssh /home/sammy

Example: rsync --archive --chown=julio:julio ~/.ssh /home/julio

### 6.- Enter to your server again using the new user:

ssh -i your_ssh_file your_new_user@your_ip_address -p your_port

Example: ssh julio@68.227.102.147 -i your_ssh_file -p 22

