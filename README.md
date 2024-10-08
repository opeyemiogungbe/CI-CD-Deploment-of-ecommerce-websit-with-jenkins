# CI-CD-Deployment-of-ecommerce-website-with-jenkins

## Overview
This project demonstrates a complete CI/CD pipeline using Jenkins to automate web application deployment. Jenkins is integrated with GitHub as the source code management tool, while Docker containerizes the application. The final Docker image is pushed to Docker Hub for future deployments. The pipeline ensures continuous integration, and continuous delivery, and automates deployment to ensure scalability and reliability.

### Table of Contents

**Prerequisites**

**Architecture**

- Step 1: Install Jenkins
- Step 2: Set up Necessary Jenkins Plugins
- Step 3: Configure Jenkins Security
- Step 4: Integrate Jenkins with GitHub
- Step 5: Configure Webhooks for Jenkins Builds
- Step 6: Create Jenkins Freestyle Job
- Step 7: Create Jenkins Pipeline Script
- Step 8: Build Docker Images in Jenkins
- Step 9: Running the Docker Container
- Step 10: Push Docker Images to a Registry
- Step 11: Documentation

**Prerequisites**

Before we begin, we must ensure we have the following:

- Ubuntu 20.04 LTS (or similar Linux distro)
- Jenkins (latest stable version)
- GitHub account with repository for the project
- Docker (installed on the Jenkins server)
- Docker Hub account for image storage
- Jenkins Plugins:
- Git Plugin
- Docker Pipeline Plugin
- Pipeline Plugin
- GitHub Plugin

### Architecture

This pipeline works as follows:

we are going to push our code changes to the GitHub repository.
- A GitHub webhook will trigger a Jenkins build.
- Jenkins checks out the code and runs unit tests.
- Jenkins builds a Docker image of the application.
- Jenkins pushes the Docker image to Docker Hub.
- The new image can be deployed on any server using Docker.

## Step 1: Install Jenkins
To begin, we need to install Jenkins on a dedicated server. Jenkins will act as the orchestrator for your CI/CD pipeline.

1. Install Java, as Jenkins requires Java to run:
```
sudo apt update
sudo apt install openjdk-11-jdk -y
```
2. Add Jenkins Repository and install Jenkins:
```
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```
3. Start Jenkins and enable it to start at boot:
```
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

4. Access Jenkins:
Open port 8080 in inbound rules on jenkins server to enable us access it on web browser

![Screenshot 2023-11-08 083515](https://github.com/user-attachments/assets/b7b44a56-bd28-4e49-8e03-4d45b707a2b3)

Open Jenkins in a web browser: http://<your-server-ip>:8080

We are going to cat into /var/lib/jenkins/secrets/initialAdminPassword to get our password

## Step 2: Set up Necessary Jenkins Plugins

Once Jenkins is installed, install the following plugins:

- Git Plugin (to integrate with GitHub).
- Docker Pipeline Plugin (to enable Docker commands within Jenkins).
- Pipeline Plugin (to write pipeline-as-code with Jenkinsfile).
- GitHub Plugin (to integrate webhooks from GitHub).

Navigate to:

Manage Jenkins > Manage Plugins > Available and search for the required plugins.

## Step 3: Configure Jenkins Security

1. Create a Jenkins User to avoid using the default admin account:

  - Go to Manage Jenkins > Manage Users > Create User.

2. Set Global Security Settings:

  - Manage Jenkins > Configure Global Security
  - Enable Jenkins' own user database for security.
  - Configure roles and permissions as needed.

3. Add Credentials:

- You’ll need to store credentials for GitHub, Docker Hub, and possibly other services like cloud providers.

  Go to Manage Jenkins > Manage Credentials to add credentials such as GitHub access tokens and Docker Hub login details.
  
## Step 4: Integrate Jenkins with GitHub

Jenkins needs to pull your source code from GitHub.

1. Install GitHub Plugin via the Jenkins plugin manager.

2. Create a GitHub Repository and clone it:
  ```
  git clone https://github.com/yourusername/yourapp.git
  ```
3. Configure GitHub in Jenkins Job:
  - When creating a Jenkins job, under "Source Code Management", select Git.
  - Provide the GitHub repository URL.
  - Add credentials (Personal Access Token) for authentication.

## Step 5: Configure Webhooks for Jenkins Builds

To automate the build trigger:

1. Go to Your GitHub Repository:

  - Navigate to Settings > Webhooks > Add webhook.
  - Set the Payload URL to http://your-jenkins-url:8080/github-webhook/.

  - In Jenkins, configure the job to trigger builds using webhooks:
    Check the box for GitHub hook trigger for GITScm polling.

## Step 6: Create Jenkins Freestyle Job
A Freestyle Job can be used to build the web application and run unit tests:

1. Go to Jenkins Dashboard and click New Item > Freestyle Project.

2. Set the GitHub Repository under "Source Code Management".

3. Add Build Steps to run unit tests or any other tasks

4. Configure Post-build Actions to archive artifacts or notify teams.

## Step 7: Create Jenkins Pipeline Script

This is a more advanced setup where you define a Jenkins pipeline using code.

Create a New Pipeline Job:

Go to New Item > Pipeline.
Write the Pipeline Script:






























