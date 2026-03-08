# A Comprehensive Guide to Web Hosting on DigitalOcean and AWS

This document provides a consolidated overview of web hosting concepts and step-by-step guides for deploying applications on DigitalOcean and AWS.

## 1. General Hosting Concepts

### 1.1. Domains and DNS

-   **Domain**: A unique, human-readable address for a website (e.g., `example.com`).
-   **Subdomain**: An extension that lives on your primary domain (e.g., `blog.example.com`). It can point to a completely different server or application.
-   **Name Servers (NS)**: Servers that store DNS records for a domain. You typically point your domain registrar (like Namecheap or GoDaddy) to the name servers of your hosting provider (like DigitalOcean or AWS).

### 1.2. Common DNS Records

DNS records tell domain name servers how to route requests.
-   **`A` Record**: Maps a domain or subdomain directly to an IPv4 address (e.g., `example.com` -> `192.0.2.1`).
-   **`CNAME` (Canonical Name) Record**: Maps a domain or subdomain to another domain name. It should not point to an IP address.
-   **`MX` (Mail Exchanger) Record**: Directs email to a mail server.
-   **`NS` Record**: Specifies the authoritative name servers for the domain.

## 2. Hosting a Node.js App on DigitalOcean (Step-by-Step)

This guide walks through setting up a secure server from scratch on a DigitalOcean droplet to run a Node.js application.

### Step 1: Initial Droplet Setup

A **Droplet** is a virtual private server (VPS) from DigitalOcean—an isolated slice of a physical server that you control.

1.  **Create an Account**: Sign up for DigitalOcean.
2.  **Create a Droplet**:
    -   **Choose an Image**: Select an operating system. **Ubuntu LTS** (Long-Term Support) is a popular choice.
    -   **Choose a Plan**: Start with a basic, cheap plan. You can resize later.
    -   **Choose a Datacenter Region**: Pick one that is geographically closest to your users.
    -   **Authentication**: Select **SSH keys**. This is more secure than using passwords.

### Step 2: Authentication and User Setup

#### 2.1. Create and Add an SSH Key
SSH (Secure Shell) allows you to securely connect to your server. It uses a key pair: a public key that lives on the server and a private key that stays on your computer.

1.  **Generate a Key Pair** (if you don't have one):
    ```bash
    # Run this on your local machine
    ssh-keygen -t rsa -b 4096
    # When prompted, save it to a file like ~/.ssh/do_key
    ```
2.  **Add the Public Key to DigitalOcean**: Copy the contents of your **public** key file (`~/.ssh/do_key.pub`) and add it to your DigitalOcean account under `Settings > Security > SSH Keys`.
3.  When creating your droplet, select this SSH key under the "Authentication" section.

#### 2.2. Initial Server Login
Connect to your new server for the first time as the `root` user.
```bash
# On your local machine. Replace with your droplet's IP.
ssh root@<your_server_ip>
```

#### 2.3. Create a Non-Root User
Operating as `root` is risky. It's best practice to create a separate user with administrative privileges.

1.  **Create the user**:
    ```bash
    # On the server
    adduser mel
    ```
    You will be prompted to create a password (e.g., `<secret>`) and fill in user information (you can leave most of it blank).

2.  **Grant Administrative Privileges**: Add the new user to the `sudo` group. This allows them to run commands with `sudo` (Super-User DO).
    ```bash
    # On the server
    usermod -aG sudo mel
    ```

3.  **Switch to the New User**:
    ```bash
    su - mel
    ```
    You are now logged in as the new user in their home directory.

#### 2.4. Disable Root Login (Security Measure)
To enhance security, disable direct login for the `root` user. Future logins must use your new user account.

1.  **Edit the SSH Daemon Configuration**:
    ```bash
    # Use sudo to edit the file
    sudo vi /etc/ssh/sshd_config
    ```
2.  Find the line `PermitRootLogin yes` and change it to `PermitRootLogin no`.
3.  **Restart the SSH Service** to apply the changes:
    ```bash
    sudo service sshd restart
    ```
Now, if you `exit` and try to `ssh root@<ip>`, the connection will be refused. You must now log in as `ssh mel@<ip>`.

### Step 3: Install a Web Server (Nginx)

Nginx is a high-performance web server. We will use it as a **reverse proxy**—it will receive public traffic on standard ports (80/443) and forward it to our Node.js application running on an internal port (e.g., 3000).

1.  **Update and Install Nginx**:
    ```bash
    # On the server
    sudo apt update
    sudo apt install nginx
    ```
2.  **Start Nginx**:
    ```bash
    sudo service nginx start
    ```
    If you visit your server's IP address in a browser, you should see the "Welcome to nginx" page.

3.  **Configure the Reverse Proxy**: Edit the default Nginx configuration file.
    ```bash
    sudo vi /etc/nginx/sites-available/default
    ```
    Find the `location / { ... }` block and modify it to proxy requests to your future Node.js app.
    ```nginx
    location / {
        # First, try to serve request as file, then
        # as directory, then fall back to displaying a 404.
        # try_files $uri $uri/ =404; # Comment out or remove this line.

        # Add this line to forward traffic to your Node app
        proxy_pass http://127.0.0.1:3000;
    }
    ```
4.  **Reload Nginx** to apply the configuration:
    ```bash
    sudo service nginx reload
    ```

### Step 4: Set Up a Node.js Application

1.  **Install Node.js and npm**:
    ```bash
    # On the server
    sudo apt install nodejs npm
    ```
2.  **Prepare the Application Directory**:
    ```bash
    # Take ownership of the web root directory
    sudo chown -R $USER:$USER /var/www

    # Create a directory for your app and navigate into it
    mkdir /var/www/app
    cd /var/www/app
    ```
3.  **Get Your App Code**: The best way is to clone it from a Git repository.
    ```bash
    # Make sure git is installed
    sudo apt install git

    # Clone your project
    git clone <your_repository_url> .
    ```
4.  **Install Dependencies**:
    ```bash
    npm install
    ```
5.  **Test the App**: Run your app to make sure it works.
    ```bash
    node app.js # Or whatever your entry file is
    ```
    Your app should now be running. Since Nginx is proxying port 80 to port 3000, visiting your domain/IP in a browser should now show your Node.js app instead of the Nginx welcome page.

### Step 5: Manage the Application with PM2

If you close your SSH session, the Node.js app will stop. A **process manager** like PM2 will keep your app running in the background, restart it if it crashes, and help manage logs.

1.  **Install PM2 Globally**:
    ```bash
    # On the server
    sudo npm install pm2 -g
    ```
2.  **Start Your App with PM2**:
    ```bash
    # Run from your app directory (/var/www/app)
    pm2 start app.js --name "my-cool-app"
    ```
3.  **Set PM2 to Start on Boot**: PM2 can generate a startup script that will resurrect your running processes after a server reboot.
    ```bash
    pm2 startup
    ```
    This command will output another command that you need to copy and run.
4.  **Save the Process List**:
    ```bash
    pm2 save
    ```

**Common PM2 Commands**:
-   `pm2 list`: Show status of all apps.
-   `pm2 stop <app_name>`: Stop an app.
-   `pm2 restart <app_name>`: Restart an app.
-   `pm2 logs <app_name>`: View logs for an app.
-   `pm2 monit`: Monitor CPU and memory usage of all apps.
-   `pm2 delete <app_name>`: Remove an app from PM2's list.

## 3. Hosting a Static Site on AWS (Overview)

This is a high-level overview of hosting a static website (HTML, CSS, JS) on AWS.

1.  **S3 (Simple Storage Service)**:
    -   Create a new S3 bucket. The bucket name must be **exactly the same** as your domain name (e.g., `www.example.com`).
    -   Upload your website files (`index.html`, etc.) to the bucket.
    -   In the bucket properties, enable "Static website hosting."
    -   In the permissions, edit the bucket policy to allow public read access. This makes the files web-accessible.

2.  **Route 53 (DNS Service)**:
    -   Create a "Hosted Zone" for your domain.
    -   Create an `A` record. Select "Alias" and point it to your S3 website endpoint.

3.  **AWS Certificate Manager (ACM)**:
    -   Request a free public SSL/TLS certificate for your domain. This will allow HTTPS traffic.

4.  **CloudFront (Content Delivery Network - CDN)**:
    -   Create a CloudFront distribution.
    -   Set the "Origin Domain" to your S3 bucket's website endpoint.
    -   Select "Redirect HTTP to HTTPS."
    -   Add your domain name as an "Alternate Domain Name" (CNAME).
    -   Select the custom SSL certificate you created in ACM.
    -   To make your S3 bucket private, create an **Origin Access Identity (OAI)** in CloudFront and update your S3 bucket policy to only allow access from that OAI.
    -   Finally, go back to Route 53 and change your `A` record to point to the CloudFront distribution instead of the S3 bucket. This routes all traffic through the CDN for better performance and security.

## 4. Appendix: Useful Commands

### Linux/Shell Commands
-   `sudo !!`: Reruns the last command with `sudo`.
-   `apt update`: Refreshes the list of available packages.
-   `apt upgrade`: Upgrades all installed packages to their latest versions.
-   `chown -R $USER:$USER /path/to/dir`: Changes the owner and group of a directory (and all its contents) to the current user.
-   `less /path/to/file`: View a file, allowing you to scroll.
-   `head <file>`: Show the first 10 lines of a file.
-   `tail <file>`: Show the last 10 lines of a file.
-   `tail -f <file>`: "Follow" a file, showing new lines as they are added (great for logs).

### `vi` Editor Commands
`vi` (or Vim) is a powerful terminal-based text editor.
1.  Press `i` to enter **Insert Mode** (where you can type text).
2.  Press `Esc` to return to **Command Mode**.
3.  In Command Mode:
    -   `:w` - Save the file.
    -   `:q` - Quit.
    -   `:wq` - Save and quit.
    -   `:q!` - Quit without saving changes.
