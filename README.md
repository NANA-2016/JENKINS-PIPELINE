# JENKINS-PIPELINE

##CREATING A PIPELINE JOB

![Screenshot 2025-06-12 175429](https://github.com/user-attachments/assets/7c70016e-856e-4fe2-9529-e4b59e5e0b56)

CONFIGURATION OF JENKINS PIPELINE

![Screenshot 2025-06-12 175639](https://github.com/user-attachments/assets/e171e725-83fb-430c-9249-de8e3c971698)

WRITING JENKINS PIPELINE SCRIPT

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

ADD INDEX HTML.FILE TO TRIGGER JENKINS TO RUN NEW BUILD
 
![image](https://github.com/user-attachments/assets/4559e9bc-d15d-47db-b8a6-1c4186181085)

PIPELINE JOB SUCCESSFULLY COMPLETED

![image](https://github.com/user-attachments/assets/53859d59-2211-4294-891f-e61f2bcc920d)
