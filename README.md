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
-  Access the Jenkins on http://<ip-address>:8080
- To know the administration password the command is sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/afe87c0f-5ae0-44ba-886d-f128fa9b42a9)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/4b2ed89c-4133-462e-8584-9ab33bd8de34)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/9a03ee15-ba15-4b06-8742-40efe3ca345f)

## install docker
- Below are the commands to install docker
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

 - unzip *
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
 
# Given global credientials in jenkins
- docker username & password given as credientials
  
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/ed0ad708-4bc9-42b2-89c3-25f52fc72c34)
 
- github token given as secret text
  
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/7b2d4f08-c124-4513-bca8-e16493daf199)
 
- sonarqube token given as secret text
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/e506b7bb-f7b4-4685-ad57-e44588a415a0)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/ad68d3a9-e09a-47f4-97b6-38ae0c542a8b)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/1de6f352-d30b-4ba8-8424-90f3c2215957)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/e562ff78-2330-44be-835f-a2d36bff6451)

## set up kubernetes using eksctl 
- create ec2 instance and add Iam role with permissions
 -ec2fullaccess
 -cloudformationFullaccess
 -IamFullaccess
 -Administrator access
  
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/1d946a1e-5fb8-405e-a888-e29c35815d00)
   
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/eaec0cef-162e-4d8e-a689-b42759c8c67e)
 
## install awscli
- commands to install awscli  
- Refer--https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
- $ sudo su
- $ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
- $ apt install unzip,   $ unzip awscliv2.zip
- $ sudo ./aws/install
         
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/ba6640ce-050e-425f-9aa5-4f8d8f613db1)
 
 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/3f9b7090-c89c-4a6e-996c-c26d3ef8f57a)
 
## install kubectl
- commands to install kubectl
- Refer--https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html
- $ sudo su
- $ curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.27.1/2023-04-19/bin/linux/amd64/kubectl
- $ ll , $ chmod +x ./kubectl  //Gave executable permisions
- $ mv kubectl /bin   //Because all our executable files are in /bin
- $ kubectl version --output=yaml

 ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/7091fad6-9450-4d14-89d2-78bd5554480a)
 
## install eksctl
- Refer--https://github.com/eksctl-io/eksctl/blob/main/README.md#installation
- $ curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
- $ cd /tmp
- $ ll
- $ sudo mv /tmp/eksctl /bin
- $ eksctl version

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/b2cbfae9-19d9-4c19-a09c-fe10ffa675e0)

 - create eks cluster
   
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/95cf228f-b45a-4268-b478-7c123cf74fda)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/af55e82f-5181-4a77-afb0-3441b495eefd)

## ARGOCD installation in eksctl
- commands to install argocd
- $ kubectl create namespace argocd
- $ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
- $ kubectl get pods -n argocd
- $ curl --silent --location -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v2.4.7/argocd-linux-amd64
- $ chmod +x /usr/local/bin/argocd
- $ kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
- $ kubectl get svc -n argocd
- $ kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
- $ echo XXXXXXX | base64 --decode

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/40eaba87-e7d2-459b-9e8f-6341cc7c895c)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/c3690805-a281-4242-82dd-af1c268a6a7d)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/e2f97dd8-5337-4efc-a81b-a904a48ecb22)

## IN JENKINS
- create a job
- given git URL and git branch and jenkins file path
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/3c93eba9-d1ba-48c8-9df5-e27b01124926)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/2575f013-19d3-4078-82ec-ba2b30f104b5)

- installed necessary plugins including docker pipeline , sonarqube scanner plugins .
- Given credentials of Docker username & password,sonarqube token,github token
- now build the job
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/2eefecc5-8637-49a3-a907-0859781f86bc)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/7b2b9974-9ebf-4c97-8b79-7aabc2731278)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/81cb5398-0b23-49ba-a356-a600eacd7573)

- In sonarqube quality check is passed
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/ee66528e-f062-4e8f-93de-ce4cc06f9caf)

## In argocd
- create an application by connecting to repository
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/e114944c-53d9-461c-bce0-c421dd035b5b)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/2db253c0-6cdb-4444-83f5-1464f7f96c32) 

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/a29c14a2-be6a-4833-bdbc-3cf1cdffc6f3)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/1ba6a3c8-9a76-4aec-b266-5384748c2eb6)
 
- created Pod
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/121dcf40-dc00-4e42-bb4d-add743afef43)

- created Deployment
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/4d74725b-64ef-4afe-b9d1-e4d0992e9a0a)

- created Service
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/88792bc0-ec22-4025-9e00-b0515a659bde)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/5281a14c-e811-44b9-a7bc-6a6c8f1c0351)

-Access the application using loadbalancer

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/e08d6a60-0694-40f5-97b5-fddd8dbf093b)

****************************************************************************************************************************************************************************** 
******************************************************************************************************************************************************************************
*******************************************************************************************************************************************************************************

## Deploying application using Docker

- packaging the code using mvn clean package command
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/f6003c60-06de-4036-8877-1996569498c6)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/2e4bb9c4-3977-445b-aead-5afac77f5f74)

- creating image using docker build command
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/8824c587-71d8-4fa6-a629-02a4fa759dfb)

![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/a6463b12-8764-4468-9b05-ee6a8617787d)

- creating container from the image created using docker build command.
  
- docker run -p $HOST_PORT:$CONTAINER_PORT --name <container_name> -t <image> : command to create container
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/7a703eea-c7d6-4709-a830-f0cb80dc3154)

- Access the application on localhost:port no
  
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/a215e791-8414-4997-863e-8718b6205508)
  
