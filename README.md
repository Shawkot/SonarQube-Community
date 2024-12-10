# SonarQube-Community
This repo contains information about installing and running the SonarQube community edition, which is a free software for static code analysis.
I will show how to configure this application using a docker image and scan a local code base. The setup consists of two parts:
  1. Configuring the SonarQube server which is the main application and contains all the necessary components.
  2. The second one is the sonar scanner CLI which is used to communicate with the server. One can use this scanner to scan the code base.

## Setting up the SonarQube server:
First, we need to configure the server before running the scanner for code analysis. The application can be downloaded and installed manually from the official page. On the other hand, we can use a docker image which has everything included for running the application. We will use the latter method.

### Step 1: Download the docker image
To run the application in a docker container, you must have docker installed and running. Make sure the docker service is active on your machine. Then, download the latest image of sonarqube using the command:
#### _sudo docker pull sonarqube_ 
Find the official docker image here: https://hub.docker.com/_/sonarqube
### Step 2: Start the container
After downloading the image, now we can run a container using the image. We will map port 9000 of the local machine to the port 9000 of the container. Use the following command to run the container:
#### _docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest_
### Step 3:
### Step 4:
