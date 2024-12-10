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
  
For detailed instructions follow the link https://docs.sonarsource.com/sonarqube-server/latest/try-out-sonarqube/ and finish creating a project on sonarqube.  
When you're done creating a project, you will have a project key and a token. You will also get a get command for running the scan. Here is the command:  
#### 
    sonar-scanner \
    -Dsonar.projectKey=Test-sonar \
	  -Dsonar.sources=. \
	  -Dsonar.host.url=http://localhost:9000 \
	  -Dsonar.token=sqp_de7b24606a3be2ceed63c9012cbdf849689415a0
Use your own token and project key.

## Setting up the sonar-scanner CLI:
