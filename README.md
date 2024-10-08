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
4. Open port 8080 in inbound rules on jenkins server to enable us access it on web browser

![Screenshot 2023-11-08 083515](https://github.com/user-attachments/assets/b7b44a56-bd28-4e49-8e03-4d45b707a2b3)

