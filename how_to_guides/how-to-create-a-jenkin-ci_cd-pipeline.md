# From Code to Deployment: Crafting a Jenkins CI/CD Pipeline

## Overview

This guide explains how to set up and optimize a Jenkins CI/CD pipeline for seamless automation of code integration, testing, and deployment, providing a step-by-step walkthrough to ensure a smooth and efficient development workflow. Additionally, it includes instructions on deploying a URL shortener app to Elastic Beanstalk (EB).

## Before you Start

Before you start, this how-to guide assumes that the user possesses a certain level of familiarity with cloud services, specifically AWS, and has a basic understanding of the following:

- Linux CLI and SSH
- Git and GitHub
- AWS Virtual Machines

### Step 1: Create an Ubuntu EC2 Instance

The Ubuntu EC2 instance will function as your Jenkins server.

#### Configure your instance with the following: 

-   **VM Image:** "Ubuntu AMI"

-   **Instance Type:** "t2.micro"

-   **Security Configuration:**
    - Port 22 (SSH)
    - Port 80 (HTTP)
    - Port 8080 (Jenkins GUI)

> 🚩 **NOTE**:
    For each port, set the source as "0.0.0.0/0" to allow traffic from any IP address.

-   **Key Pair:** Create or choose a key pair for SSH access and remember to change the RWX permissions to 600

-   **Retrieve public IP of your instance in the EC2 dashboard.**

![](images/instance.png)

### Step 2: SSH into your Jenkins Server

 #### Once the EC2 has been established, from your local server (computer) SSH into your remote Jenkins server

```
ssh -i /path/to/my-key.pem ubuntu@123.45.67.89
```

### Step 3: Install Virtual Environment

#### Use the following commands to install Java, [Jenkins](https://www.jenkins.io/doc/book/installing/linux/) and [Python](https://realpython.com/installing-python/#how-to-install-python-on-linux). 

Install Java (Jenkins requires Java to run):
```
sudo apt-get update
sudo apt-get install fontconfig openjdk-17-jre
java -version
```

Install Jenkins
```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins

```

Install Python3:
```
sudo apt-get update
sudo apt-get install python3 -y
python3 --version
sudo apt-get install python3.10-venv
```

### Step 4: Connect GitHub to your Jenkins Server

#### You will use this token to link your source code in GitHub to your Jenkins pipeline.

-  Navigate to GitHub and generate a new personal access token. 
    *   Select repo and admin:repo_hook(webhook) option

This option gives Jenkins control of the repo hooks and of your private repositories, also known as your source code files.


> 🚩 **NOTE**:  
   **Do Not** store your access token GitHub.    
   Be sure to copy and paste your key to a safe place you can access it later.  
   Securing your GitHub Personal Access Tokens (PATs) is crucial to maintaining the security of your repositories and account.


### Step 5: Create a Multibranch Build in Jenkins

1. Open your preferred browser and log into Jenkins GUI 
    *   enter http://your-server-ip:8080 in your browser
    *   log in
        *   unlock Jenkins(if required) - you may need to unlock Jenkins using the initial administrator password. 

2.  Install suggested plugins

3.  Create First Admin User

4.  Start using Jenkins
    *   Select New Item
    *   Give your build a name
    *   Select Multibranch Pipeline
    *   Add Display
    *   Add Branch Source(GitHub)
        *   Folder Credentials
        *   Validate
        *   Save
        *   Apply
    

### Step 6: Download GitHub Application Files

``` 
git clone <enter git repo URL here>
```
```
cd path/to/clone_repo
```
```
git archive -v -o <app_file_name.zip> --format=zip HEAD
```


### Step 7: Deploy to Elastic BeanStock

1.  Create a new web-server environment
    
    *  Enter the following configuration

        *   Application Name: url-shortner
        -   Environment Name: Urlshortner-env
        *   Platform: Pythom
        -   Platform Branch: 3.8
        *   Platform Version: 3.3.16
        -   Application Code: [add your zip file]

2.  Copy and Paste the generated URL code into a web browser


## See also


- [AWS Management Console](https://aws.amazon.com/console/)

- [Jeknins - Creating your first Pipeline](https://www.jenkins.io/doc/book/pipeline/)

- [Getting Started with AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/?gclid=Cj0KCQiAyKurBhD5ARIsALamXaH9zdMXPBupSm0Qj_FnicwUXF0fpBxaweJGjCt0qK-mgtfzLre_Q3caApQjEALw_wcB&trk=7251e6b1-d80c-4891-a63f-a6472921f7a3&sc_channel=ps&ef_id=Cj0KCQiAyKurBhD5ARIsALamXaH9zdMXPBupSm0Qj_FnicwUXF0fpBxaweJGjCt0qK-mgtfzLre_Q3caApQjEALw_wcB:G:s&s_kwcid=AL!4422!3!652240143514!e!!g!!elastic%20bean%20stalk!19870609179!147363462876)
