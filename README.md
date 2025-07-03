# JENKINS-PIPELINE

Install Jenkins and let it run access it from port 8080. Got to the browser and access Jenkins "http://<Public ip address>8080

![jenkins page and file ](https://github.com/user-attachments/assets/483fc12a-d718-401e-b4ec-1e6098cca21c)

## JENKINS SECURITY

Create an admin user so that not every one accesses Jenkins .

ssh -i "Nana.pem" ubuntu@ec2-16-171-159-226.eu-north-1.compute.amazonaws.com


## Install the required plugins .ie Docker and GIT plugins

![Screenshot 2025-06-18 114106](https://github.com/user-attachments/assets/bb49e333-8035-497a-9ab0-c363ca6a0c73)



## AUTOMATIC TRIGGERS FROM GIT-HUB

Create a free style job to test then add a web hook to the Jenkins repository to connect Jenkins with Git-hub sot at Jenkins can run triggers from you terminal through git hub

go to your repository-setting-webhook-add webhook

![connect to webhook](https://github.com/user-attachments/assets/e653784b-775e-4aa5-aaa8-6401a4c959eb)

## CREATING A PIPELINE JOB

![Screenshot 2025-06-12 175429](https://github.com/user-attachments/assets/7c70016e-856e-4fe2-9529-e4b59e5e0b56)

CONFIGURATION OF JENKINS PIPELINE

![Screenshot 2025-06-12 175639](https://github.com/user-attachments/assets/e171e725-83fb-430c-9249-de8e3c971698)

## WRITING JENKINS PIPELINE SCRIPT

![Screenshot 2025-06-12 181504](https://github.com/user-attachments/assets/f8e6ac96-a98e-4281-b80f-61cc8b9c3ed2)

GENERATE OWN PIPELINE SCRIPT

![Screenshot 2025-06-12 182125](https://github.com/user-attachments/assets/c665f914-9a57-482c-8eb1-c4ffb9b6d594)

REPLACE GENARATED PREVIOUS SCRIPT WITH GENERATED SCRIPT TO CONNECT JENKINS WITH GIT HUB

![Screenshot 2025-06-12 182503](https://github.com/user-attachments/assets/89b99f73-0f12-4200-8ac2-0e1dbc99e44b)

CREATE A docker.sh file FILE IN THE SAME INSTANCE AS JENKINS TO RUN DOCKER COMMANDS IN JENKINS

docker.sh FILECONTENT

<sudo apt-get update -y
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update -y
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo systemctl status docker>


![image](https://github.com/user-attachments/assets/a733f247-dffa-4094-88cd-5f2104ab8db9)

MAKE FILE EXCECUTABLE

![image](https://github.com/user-attachments/assets/28e016f8-ea3d-443e-8e8c-6a9f81ba6ef6)


CREATE DOCKER FILE TO ALLOW CREATION OF A DOCKER IMAGE

![image](https://github.com/user-attachments/assets/79da0f70-23fe-4193-9b17-4e9e6cc1c008)

## ADD INDEX HTML.FILE TO TRIGGER JENKINS TO RUN NEW BUILD
 
![image](https://github.com/user-attachments/assets/4559e9bc-d15d-47db-b8a6-1c4186181085)

### CREATE JENKINSFILE AND CONFUGURE IT TO RUN DOCKER CONTAINERS USING THE BUILD DOCKER IMAGE .

#### USE THE SCRIPT BELOW

pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-html-project'
        CONTAINER_NAME = 'jenkins-html-container'
        HOST_PORT = '8082'
        REPO_URL = 'https://github.com/NANA-2016/JENKINS-CICD-PIPELINE--PROJECT-3.git'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Simpler declarative checkout
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: "${BRANCH}"]],
                    userRemoteConfigs: [[url: "${REPO_URL}"]]
                ])
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                // Stop and remove container if it exists
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
                // Run new container
                sh "docker run -d -p ${HOST_PORT}:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        }

        stage('Verify Container is Running') {
            steps {
                // Wait a few seconds for container to start
                sh "sleep 5"
                // Check container health via curl
                sh "curl -f http://localhost:${HOST_PORT} || (echo 'Health check failed' && exit 1)"
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
        // Uncomment this block later when you want automatic cleanup
        /*
        always {
            echo 'Cleaning up...'
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
                sh "docker rmi ${IMAGE_NAME} || true"
            }
        }
        */
    }
}




## ADD INDEX HTML.FILE TO TRIGGER JENKINS TO RUN NEW BUILD
 
![image](https://github.com/user-attachments/assets/4559e9bc-d15d-47db-b8a6-1c4186181085)

## CONFIGURE THE ACCESSPORT TO 8082 ON YOUR INSTANCE

![ASCCESSPORTFOR INDEXHTML](https://github.com/user-attachments/assets/1ea1a50a-3c15-4460-8653-890c1de803fc)

## PIPELINE JOB SUCCESSFULLY COMPLETED

![image](https://github.com/user-attachments/assets/53859d59-2211-4294-891f-e61f2bcc920d)

### YOU CAN NOW ACCESSTHE Index.htmlfile through the browser .

using 

http://<your-ec2-public-ip>:8082

![Screenshot 2025-07-03 180237](https://github.com/user-attachments/assets/0b9e14a8-d045-409e-8daf-0efb450a83ab)

