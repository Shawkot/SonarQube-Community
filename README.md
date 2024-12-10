# SonarQube-Community
This repo contains information about installing and running the SonarQube community edition, which is a free software for static code analysis.
I will show how to configure this application using a docker image and scan a local code base. The setup consists of two parts:
  1. Configuring the SonarQube server which is the main application and contains all the necessary components.
  2. The second one is the sonar scanner CLI which is used to communicate with the server. One can use this scanner to scan the code base.

## Setting up the SonarQube server:
First, we need to configure the server before running the scanner for code analysis. The application can be downloaded and installed manually from the official page. On the other hand, we can use a docker image which has everything included for running the application. We will use the later method.

### Step 1: Download the docker image
To run the application in a docker container, you must have docker installed and running. Make sure the docker service is active in your machine. Then, download the latest image of sonarqube using the command:
sudo docker pull sonarqube
Find the official docker image here: https://hub.docker.com/_/sonarqube
### Step 1:
### Step 1:
### Step 1:
