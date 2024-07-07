# Jenkins CI/CD Pipeline To Deploy Angular App

## Overview
To set up a multibranch pipeline in Jenkins that deploys applications to a Tomcat server with different environments (test and production) using the provided GitHub repositories and Nginx for reverse proxy

### Required Instances:
- **Jenkins server**: t2.medium, Ubuntu Linux, ap-south-1b
- **SonarQube server**: t2.small, Ubuntu Linux, ap-south-1a
- **Tomcat server**: t2.micro, Ubuntu Linux, ap-south-1a


## Stage 1: Install and Configure Jenkins Server

### Step 1: Install Jenkins

1. **Add the Jenkins repository key to your system:**
    ```sh
    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo gpg --dearmor -o /usr/share/keyrings/jenkins.gpg
    ```

2. **Append the Debian package repository address to your sources.list:**
    ```sh
    sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins.gpg] http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    ```

3. **Update apt repository and install Jenkins:**
    ```sh
    sudo apt update
    sudo apt install jenkins -y
    ```
    ### Step 2: Start Jenkins

1. **Start Jenkins using systemctl:**
    ```sh
    sudo systemctl start jenkins.service
    ```

2. **Verify Jenkins status:**
    ```sh
    sudo systemctl status jenkins
    ```

### Step 3: Open the Firewall

1. **Allow Jenkins through the firewall on port 8080:**
    ```sh
    sudo ufw allow 8080
    ```

2. **Ensure OpenSSH is allowed and enable the firewall:**
    ```sh
    sudo ufw allow OpenSSH
    sudo ufw enable
    ```
