## Install Jenkins, configure Docker as slave, set up cicd, deploy applications to k8s using Argo CD in GitOps way.
- create ec2 instance
## install jenkins
- Pre-Requisites:
   - java
## Run the below commands to install java & jenkins
- Install java
  - sudo apt update
  - sudo apt install openjdk-11-jre
    ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/9089b8a8-3220-4b3d-8d2c-ad34fea86996)
- Verify Java is Installed
   - java -version
- Installing jenkins
- curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
- echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
- sudo apt-get update
- sudo apt-get install jenkins
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/142a7c20-1fac-4d72-8c66-4086a229afb5)
- Allow the inbound rule with port 8080 as jenkins by default runs on port 8080.
- To know the administration password the command is sudo cat /var/lib/jenkins/secrets/initialAdminPassword
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/afe87c0f-5ae0-44ba-886d-f128fa9b42a9)
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/4b2ed89c-4133-462e-8584-9ab33bd8de34)
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/9a03ee15-ba15-4b06-8742-40efe3ca345f)
## install docker
- command to install docker
- sudo apt update
- sudo apt install docker.io
- ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/87ddf889-1e6d-4c56-b132-fbf600f12c29)

## Grant Jenkins user and Ubuntu user permission to docker deamon.
- sudo su - 
- usermod -aG docker jenkins
- usermod -aG docker ubuntu
- systemctl restart docker
## install sonarqube
- sudo su - 
 -apt install unzip
 -adduser sonarqube
  ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/c150df1e-e46e-4453-9d84-c50d573e78b8)

 -wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/9ba0e17f-c3ff-4302-b849-bcf9aa8fc463)

 -unzip *
 - chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
 - chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
 - cd sonarqube-9.4.0.54424/bin/linux-x86-64/
 - ./sonar.sh start
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/9460bf93-3f99-495b-985f-f11d4aede3de)
- Access the SonarQube Server on http://<ip-address>:9000
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/ae893bb2-bd29-4741-82cb-39c5bb010d13)

## install necessary plugins in jenkins
- install docker-pipeline plugin 
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/c2126938-faf9-4704-8a41-a07d240e7c14)
- install sonarqube scanner plugin
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/30e5dca6-024a-4e75-a262-fddfa5e0d268)
## Given global credientials in jenkins
- docker username & password given as credientials
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/ed0ad708-4bc9-42b2-89c3-25f52fc72c34)
- github token given as secret text
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/7b2d4f08-c124-4513-bca8-e16493daf199)
- sonarqube token given as secret text
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/ad68d3a9-e09a-47f4-97b6-38ae0c542a8b)
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/1de6f352-d30b-4ba8-8424-90f3c2215957)
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/e562ff78-2330-44be-835f-a2d36bff6451)
 
 
 
