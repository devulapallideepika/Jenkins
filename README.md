# Install Jenkins, configure Docker as slave, set up cicd, deploy applications to k8s using Argo CD in GitOps way.
- create ec2 instance
# install jenkins
- Pre-Requisites:
   - java
# Run the below commands to install java & jenkins
- Install java
  - sudo apt update
  - sudo apt install openjdk-11-jre
    ![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/9089b8a8-3220-4b3d-8d2c-ad34fea86996)

- Verify Java is Installed
   - java -version
- Installing jenkins
- curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
- sudo apt-get update
- sudo apt-get install jenkins
![image](https://github.com/devulapallideepika/Jenkins/assets/129947829/142a7c20-1fac-4d72-8c66-4086a229afb5)
