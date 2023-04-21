# Ubuntu-22.04-Web-Server-Setup
 Describes the linux commands needed to set up a web server on ubuntu 22.04
 
## Initial Server Setup with Ubuntu 22.04 - taken from:
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04

Step 1 — Logging in as root
$ ssh root@your_server_ip -i your_ssh_file -p your_port

Step 2 — Creating a New User
adduser your_new_user
Example: $ adduser julio // Add an ubuntu user. This can be your name or just user

Step 3 — Granting Administrative Privileges
usermod -aG sudo your_new_user
Example: $ usermod -aG sudo julio
Note: You can now type sudo before commands to run them with superuser privileges when logged in as your regular user.

Step 4 — Setting Up a Firewall
$ ufw app list // examine the list of installed UFW profiles
$ ufw allow OpenSSH  //  Allows SSH connections.
$ ufw allow 2221/tcp
$ sudo ufw allow http // This is the same as ufw allow 80/tcp
$ sudo ufw allow https // This is the same as ufw allow 443/tcp
$ ufw enable // Enable the firewall
$ ufw status // See that SSH connections are still allowed

Step 5 — Enabling External Access for Your Regular User

If the root Account Uses SSH Key Authentication

To log in as your regular user with an SSH key, you must add a copy of your local public key to your new user’s ~/.ssh/authorized_keys file.

Since your public key is already in the root account’s ~/.ssh/authorized_keys file on the server, you can copy that file and directory structure to your new user account using your current session.

The simplest way to copy the files with the correct ownership and permissions is with the rsync command. This command will copy the root user’s .ssh directory, preserve the permissions, and modify the file owners, all in a single command. Make sure to change the highlighted portions of the command below to match your regular user’s name:

Go to the home directory of your root user account and run this, change sammy for your new user.
rsync --archive --chown=sammy:sammy ~/.ssh /home/sammy
Example: rsync --archive --chown=julio:julio ~/.ssh /home/julio

6.- Enter to your server again using the new user:

 ssh -i your_ssh_file your_new_user@your_ip_address -p your_port
Example: ssh -i digital_ocean_ssh.txt julio@64.226.101.144 -p 22

