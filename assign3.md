# Assignment 3

## Setting up a Debian 12 Server with Digital Ocean

These instructions will be a guide for to process you through how to set up a new Debian 12 Server with the use of Digital Ocean. This document will include steps on creating a new regular user with admin privileges, preventing root access via SSH, installing nginx, and configuring it to serve a sample website. 

## Step 1: Create a New Regular User

### Login to your user using your SSH key as root user using this command in your terminal. Remember to replace ‘your_ip_address’ with the actual IP address of your droplet.

```bash

ssh root@your_ip_address
```

## Step 2: Give the user administrative priveleges

### Once you have successfully logged in, create a new regular user with the following command. Remember to replace <username> with your preferred username.

```bash
adduser <username>
```

### After you have created a new user, Add the user to the sudo group and give that user administrative privileges using this command:

```bash
usermod -aG sudo <username>
```

### Next, you want to set the user’s shell to bash using this command:

```bash
chsh -s /bin/bash <username>
```

## Step 3: Prevent Root SSH Access

### Open the SSH daemon configuration file with a text editor using this command:

```bash
vim /etc/ssh/sshd.config
```

### Find the line that says ‘PermitRootLogin’ and change it to **no:**

```bash
PermitRootLogin no
```

### After you have changed PermitRootLogin to no, restart your SSH server with this command:

```bash
systemctl restart ssh
```

## Step 4: Install Nginx

### In this step, we will be installing nginx

### Firstly, we will update your package lists using this command:

```bash
sudo apt update
```

### Once that is finished, we will proceed with installing Nginx using this command:

```bash
sudo apt install nginx
```

## Step 5: Configure Nginx to serve a sample website

### Create a new configuration file for your website using the following command:

```bash
sudo vim /etc/nginx/sites-available/mywebsite
```

### In the configuration file, add a similar script like the one below. Remember to replace ‘your-domain’ with your domain or IP address.

```bash
server {
    listen 80;
    server_name your_domain;

    location / {
        root /var/www/html;
        index index.html;
    }
}
```

### Once that is completed, create a symbolic link to your new configuration file with the following command:

```bash
sudo ln -s /etc/nginx/sites-available/mywebsite /etc/nginx/sites-enabled/
```

## Step 6: Test your configuration file

### Once you have successfully created a symbolic link in sites-enabled, test the Nginx configuration with this command:

```bash
sudo nginx -t
```

### If the test is successful with no errors, reload Nginx to apply your changes:

```bash
sudo systemctl restart nginx
```

## Congratulations! Your Debian 12 server is now set up with a new regular user, root SSH access has been disables, you installed Nginx, and a sample website has been configured.