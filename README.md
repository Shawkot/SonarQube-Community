# SonarQube-Community
This repo contains information about installing and running the SonarQube community edition, which is a free software for static code analysis.
I will show how to configure this application using a docker image and scan a local code base. The setup consists of two parts:
  1. Configuring the SonarQube server which is the main application and contains all the necessary components.
  2. The second one is the sonar scanner CLI which is used to communicate with the server. One can use this scanner to scan the code base.

## Setting up the SonarQube server:
First, we need to configure the server before running the scanner for code analysis. The application can be downloaded and installed manually from the official page. On the other hand, we can use a docker image which has everything included for running the application. We will use the latter method.

### Step 1: Download the docker image
To run the application in a docker container, you must have docker installed and running. Make sure the docker service is active on your machine. Then, download the latest image of sonarqube using the command:
#### 
    sudo docker pull sonarqube
Find the official docker image here: https://hub.docker.com/_/sonarqube
### Step 2: Start the container
After downloading the image, now we can run a container using the image. We will map port 9000 of the local machine to the port 9000 of the container. Use the following command to run the container:
#### 
    docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest
### Step 3: Log in to the web UI
At this point, the sonarqube server is running in a container. The application provides a UI to manage all the settings ranging from administration to real scanning. It also provides a nice overview of a scan. To log in to the web interface, 
- visit HTTP://localhost:9000 and the default "username/password" is "admin/admin"
- Then change the default password immediately.
### Step 4: Create a project
Now, to scan a local repo, you need to create a project first and you can do that from the web interface. Creating the project involves,
- creating a project key
- generating a token for authentication
  
For detailed instructions follow the link https://docs.sonarsource.com/sonarqube-server/latest/try-out-sonarqube/ and finish creating a project on sonarqube. When you're done creating a project, you will have a project key and a token. You will also get a get command for running the scan. Here is the command:  
#### 
    sonar-scanner \
    -Dsonar.projectKey=Test-sonar \
    -Dsonar.sources=. \
    -Dsonar.host.url=http://localhost:9000 \
    -Dsonar.token=sqp_de7b24606a3be2ceed63c9012cbdf849689415a0
Use your own token and project key.

## Setting up the sonar-scanner CLI:
So far, we have configured the sonarqube server and created all the required components like token and project key to talk with the server. Now, we need a client software which can run the scan and can communicate to the server. Then the server will show the result on the web UI. We will use the _sonar-scanner_ CLI application. Follow the steps below to setup the client application.
### Step 5: Download the sonar-scanner CLI application
Download the client application from the following link:  
https://docs.sonarsource.com/sonarqube-community-build/analyzing-source-code/scanners/sonarscanner/  
Download the appropriate application based on your system. Then, unzip the application.
### Step 6: Setting up the client
In the previous step, you unzip the application and you will find a _conf_ folder, which consists of a file called "sonar-scanner.properties". In this file, you can configure all the required
arguments to run the client application. For example, the host URL, token for authentication, and so on. You can also supply these applications when running the command 'sonar-scanner' as shown before. On the other hand, you can also create environment variables for those values like tokens and so on. Follow the link below for detailed instructions:  
https://docs.sonarsource.com/sonarqube-community-build/analyzing-source-code/scanners/sonarscanner/  
But, for convenience, I added all the argument values in the 'sonar-scanner.properties' file like this:  
####
    sonar.host.url=http://localhost:9000
    sonar.projectKey=Test-sonar
    sonar.token=sqp_a3e450c41f7ea9cxbf68ac0950912b2a3c52807d
    sonar.sources=.

### Step 7:
