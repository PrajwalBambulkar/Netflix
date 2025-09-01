  <div align="center">
  <a href="http://netflix-clone-with-tmdb-using-react-mui.vercel.app/">
    <img src="./public/assets/netflix-logo.png" alt="Logo" width="100" height="32">
  </a>

  <h3 align="center">Netflix Clone</h3>

  <p align="center">
    <a href="https://netflix-clone-react-typescript.vercel.app/">View Demo</a>
    ·
    <a href="https://github.com/crazy-man22/netflix-clone-react-typescript/issues">Report Bug</a>
    ·
    <a href="https://github.com/crazy-man22/netflix-clone-react-typescript/issues">Request Feature</a>
  </p>
</div>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#prerequests">Prerequests</a>
    </li>
    <li>
      <a href="#which-features-this-project-deals-with">Which features this project deals with</a>
    </li>
    <li><a href="#third-party-libraries-used-except-for-react-and-rtk">Third Party libraries used except for React and RTK</a></li>
    <li>
      <a href="#contact">Contact</a>
    </li>
  </ol>
</details>

<br />

<div align="center">
  <img src="./public/assets/home-page.png" alt="Logo" width="100%" height="100%">
  <p align="center">Home Page</p>
  <img src="./public/assets/mini-portal.png" alt="Logo" width="100%" height="100%">
  <p align="center">Mini Portal</p>
  <img src="./public/assets/detail-modal.png" alt="Logo" width="100%" height="100%">
  <p align="center">Detail Modal</p>
  <img src="./public/assets/grid-genre.png" alt="Logo" width="100%" height="100%">
  <p align="center">Grid Genre Page</p>
  <img src="./public/assets/watch.png" alt="Logo" width="100%" height="100%">
  <p align="center">Watch Page with customer contol bar</p>
</div>

## Prerequests

- Create an account if you don't have on [TMDB](https://www.themoviedb.org/).
  Because I use its free API to consume movie/tv data.
- And then follow the [documentation](https://developers.themoviedb.org/3/getting-started/introduction) to create API Key
- Finally, if you use v3 of TMDB API, create a file named `.env`, and copy and paste the content of `.env.example`.
  And then paste the API Key you just created.

## 🚀 Tech Stack
- **GitHub** → Source Code Management  
- **Jenkins** → Continuous Integration (CI)  
- **Docker** → Containerization  
- **SonarQube** → Code Quality & Static Analysis  
- **Trivy** → Filesystem & Image Security Scan  
- **OWASP Dependency Check** → Dependency Scanning  
- **Terraform** → Infrastructure as Code (EKS)  
- **Kubernetes (EKS)** → Container Orchestration  
- **Prometheus + Grafana** → Monitoring & Visualization  

## Steps:-

Step 1 — Launch an Ubuntu(22/24.04) T2 Large Instance with 30GB, create IAM role and attach admin permissions

Step 2 — Install Jenkins, Docker and Trivy. Create a Sonarqube Container using Docker.

Step 3 — Create a TMDB API Key.

Step 4 — Install Prometheus and Grafana On the new Server.

Step 5 — Install the Prometheus Plugin and Integrate it with the Prometheus server.

Step 6 — Email Integration With Jenkins and Plugin setup.

Step 7 — Install Plugins like JDK, Sonarqube Scanner, Nodejs, and OWASP Dependency Check.

Step 8 — Create a Pipeline Project in Jenkins using a Declarative Pipeline

Step 9 — Install OWASP Dependency Check Plugins

Step 10 — Docker Image Build and Push

Step 11 — Deploy the image using Docker

Step 12 — Setup AWS EKS with Terraform

Step 13 — Access the Netflix app on the Browser.

Step 14 — Terminate the AWS EC2 Instances.

## 📝 Steps to Deploy
Step 1: Setting up AWS EC2 Instance
----------------------------------
Creating an EC2 instance t2.large with Ubuntu 24 AMI, t2.large, and 30 GB storage




vi script1.sh
## Setup Script

- Install **Terraform,kubectl,Aws cli**


```bash
#!/bin/bash
#install terraform
sudo apt install wget -y
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

#install Kubectl on Jenkins
sudo apt update
sudo apt install curl -y
curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client

#install Aws cli
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt-get install unzip -y
unzip awscliv2.zip
sudo ./aws/install

```
=======================================================



Step 2 — Install Jenkins, Docker and Trivy
-------------------------------------------

Script2 for Java,Jenkins,Docker

vi script2.sh

```bash
#!/bin/bash
sudo apt update -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins

#install docker
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg -y
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker ubuntu
newgrp docker
```

## vi trivy.sh
```bash

sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y
```


Job 1: EKS Provision
-----------------------

Create a S3 private bucket for statefile : neetflix

Install terraform plugin

let’s find the path to our Terraform (we will use it in the tools section of Terraform)

In EC2 instance run the below command

which terraform 

Now --> Manage Jenkins –> Tools

Terraform --> Name: terraform, uncheck install automatically , install directory = /usr/bin/

Now create a new pipeline job for the Eks provision
------------------------------------------

New Item --> Pipeline --> EKSJOB 

This project is parameterized  
Name: action  
choices:  
- apply  
- destroy  

```bash
pipeline{
    agent any
    stages {
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/ReyazShaik/devsecops-netflix.git'
            }
        }
        stage('Terraform version'){
             steps{
                 sh 'terraform --version'
             }
        }
        stage('Terraform init'){
             steps{
                 dir('EKS_TERRAFORM') {
                      sh 'terraform init'
                   }
             }
        }
        stage('Terraform validate'){
             steps{
                 dir('EKS_TERRAFORM') {
                      sh 'terraform validate'
                   }
             }
        }
        stage('Terraform plan'){
             steps{
                 dir('EKS_TERRAFORM') {
                      sh 'terraform plan'
                   }
             }
        }
        stage('Terraform apply/destroy'){
             steps{
                 dir('EKS_TERRAFORM') {
                      sh 'terraform ${action} --auto-approve'
                   }
             }
        }
    }
}
```
Run the above Pipeline in jenkins.

-Run this command in Linux Machine
aws eks list-clusters --region ap-south-1

aws eks update-kubeconfig --region ap-south-1 --name EKS_CLUSTER


Now Run sonarqube container
=============================
```bash
sudo chmod 777 /var/run/docker.sock
systemctl daemon-reload
systemctl restart docker.service

docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```




Step 3: Create a TMDB API Key to get the movie data automatically from their database
=====================================================================================

Next, we will create a TMDB API key

Open a new tab in the Browser and search for TMDB , signup first and login

--> Settings --> API --> Create --> Developer --> Application Name = demo, rest bla bla bla

cacc35c61cd76805987aca08d540f24e


Step 4 — Install Prometheus , Grafana and Node Exporter On the Ubuntu 24 t2.medium
===========================================================

Launch a new Ubuntu 24 t2.medium for Promo and Grafana

Install Promotheus
=================

vi promo.sh
```bash
sudo apt update
sudo useradd --system --no-create-home --shell /bin/false prometheus
wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz
tar -xvf prometheus-2.47.1.linux-amd64.tar.gz
sudo mkdir -p /data /etc/prometheus
cd prometheus-2.47.1.linux-amd64/
sudo mv prometheus promtool /usr/local/bin/
sudo mv consoles/ console_libraries/ /etc/prometheus/
sudo mv prometheus.yml /etc/prometheus/prometheus.yml
sudo chown -R prometheus:prometheus /etc/prometheus/ /data/
cd
rm -rf prometheus-2.47.1.linux-amd64.tar.gz
prometheus --version
```
---------------------------------------------------------
```bash
sudo vi /etc/systemd/system/prometheus.service

[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target
StartLimitIntervalSec=500
StartLimitBurst=5
[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/data \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090 \
  --web.enable-lifecycle
[Install]
WantedBy=multi-user.target
```
---------------------------------

sudo systemctl enable prometheus

sudo systemctl start prometheus

sudo systemctl status prometheus

journalctl -u prometheus -f --no-pager   [to check logs]



Install Node Exporter
=====================

vi nodeexp.sh
```bash
sudo useradd --system --no-create-home --shell /bin/false node_exporter
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz
sudo mv node_exporter-1.6.1.linux-amd64/node_exporter /usr/local/bin/
rm -rf node_exporter*
node_exporter --version
```

sudo vi /etc/systemd/system/node_exporter.service
```bash
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target
StartLimitIntervalSec=500
StartLimitBurst=5
[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/node_exporter \
    --collector.logind
[Install]
WantedBy=multi-user.target
```
---------------------------------------------
```bash
sudo systemctl enable node_exporter

sudo systemctl start node_exporter

sudo systemctl status node_exporter

journalctl -u node_exporter -f --no-pager  [for any errors]
```

sudo vi /etc/prometheus/prometheus.yml  
```bash
- job_name: node_export
    static_configs:
      - targets: ["localhost:9100"]
```
promtool check config /etc/prometheus/prometheus.yml     [check if the config is valid.]

curl -X POST http://localhost:9090/-/reload          [POST request to reload the config.]

http://<ip>:9090/targets



Install Grafana
================

vi Grafana.sh
```bash
sudo apt-get install -y apt-transport-https software-properties-common
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
sudo apt-get update
sudo apt-get -y install grafana
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
sudo systemctl status grafana-server

```

[http://IP:9100 --> node exporter is working
http://IP:9090 --> Promo is working

http://Ip:3000 --> Grafana, username: admin, password: admin](http://13.233.215.35:9100  
--> Node Exporter is working  

http://13.233.215.35:9090  
--> Prometheus is working  

http://<IP>:3000  
--> Grafana  
   Username: admin  
   Password: admin  
)


To visualize metrics, you need to add a data source first.

Click Add data source and select Prometheus--> URL : http://localhost:9090  (as we have in same server)

Let’s add Dashboard --> top right corner --> + --> import Dashboard paste this code 1860 and  --> promotheus --> click on load


Step 5 — Install the Prometheus Plugin and Integrate it with the Prometheus server
===================================================================================

Goto Manage Jenkins –> Plugins –> Available Plugins --> Prometheus and install it and restart

To create a static target, you need to add job_name with static_configs 

Go to Prometheus server

sudo vi /etc/prometheus/prometheus.yml

  - job_name: 'jenkins'
    metrics_path: '/prometheus'
    static_configs:
      - targets: ['<jenkins-ip>:8080']


promtool check config /etc/prometheus/prometheus.yml



sudo systemctl restart Prometheus



curl -X POST http://localhost:9090/-/reload

http://<ip>:9090/targets

Click On Dashboard –> + symbol –> Import Dashboard --> Use Id 9964 and click on load


Step 6 — Email Integration With Jenkins and Plugin Setup
===========================================================

Install Email Extension Plugin in Jenkins

Go to your Gmail and click on your profile

Then click on Manage Your Google Account –> click on the security tab on the left side panel you will get this page(provide mail password).

2-step verification should be enabled.

Search for the word "app" in the search bar 

App Name = Jenkins 

guyyqkpaqhknshpk


Once the plugin is installed in Jenkins, click on manage Jenkins –> configure system there under the E-mail Notification section configure the details

E-mail Notification

SMTP Server ---> smtp.gmail.com
Advanced --> Use SMTP authentication
Username = trainerreyaz@gmail.com
password = guyyqkpaqhknshpk (the generated password not your gmail pwd)
use ssl
SMTP port = 465

Test


Click on Manage Jenkins–> credentials and add your mail username and generated password
Kind = username and pwd
username = trainerreyaz@gmail.com
pwd= guyyqkpaqhknshpk (generated pwd)
ID = mail
Desc = mail


This is to just verify the mail configuration

Now under the Extended E-mail Notification section configure the details as shown in the below images


Extended E-mail Notification
SMTP server = smtp.gmail.com
SMTP port = 465
Advance = select mail
use ssl
Default triggers

always
failure-any



Step 7 — Install Plugins like JDK, Sonarqube Scanner, NodeJs, OWASP Dependency Check
===================================================================================

Install Plugin
Goto Manage Jenkins →Plugins → Available Plugins →

Install below plugins

Eclipse Temurin Installer (Install without restart)

SonarQube Scanner (Install without restart)

NodeJs Plugin (Install Without restart)

Docker

Docker Commons

Docker Pipeline

Docker API

Docker-build-step

Goto Manage Jenkins → Tools → Install JDK(23) and NodeJs(23)→ Click on Apply and Save

JDK installations --> Add JDK --> Name: jdk23, remove install oracle and add Install from adoptium.net and select jdk-23+37 (install automatically)

SonarQube Scanner installations --> Add SonarQube Scanner --> Name=sonar-scanner, install automatically --> version: sonarscanner 7.1 latest

NodeJS installations --> Add NodeJS --> install automatically --> install from nodejs.org -> version nodejs 16.2.0

Docker installations --> Name = docker --> install automatically --> Add installer --> select docker.com --> latest



Configure Sonar Server in Manage Jenkins
==========================================

Go to your Sonarqube Server. http://ip:9000

Click on Administration → Security → Users → Click on Tokens and Update Token → Give it a name netflix → and click on Generate Token

squ_c3c2b101de5c65dabc210f1393e8789d585b6d15

Goto Jenkins Dashboard → Manage Jenkins → Credentials → Add Secret Text.
Kind = Secret Text
Scope = Global
Secret = Paste the sonar key you copied
ID = sonar-token
Desc = sonar-token

Adding sonar server details in Jenkins
---------------------------------

Now, go to Dashboard → Manage Jenkins → System --> SonarQube servers
Name = sonar-server
Server URL = http://35.154.52.225:9000
Server authentication token = sonar-token that you created in credentials

In the Sonarqube Dashboard add a quality gate
------------------------------------------

Administration–> Configuration–>Webhooks --> create 
Name = Jenkins
URL = http://35.154.52.225:8080/sonarqube-webhook/
Secret = empty

Create a Pipeline 
===================

pipeline{
    agent any
    tools{
        jdk 'jdk23'
        nodejs 'node23'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/ReyazShaik/devsecops-netflix.git'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=netflix \
                    -Dsonar.projectKey=netflix '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
    }
    post {
     always {
        emailext attachLog: true,
            subject: "'${currentBuild.result}'",
            body: "Project: ${env.JOB_NAME}<br/>" +
                "Build Number: ${env.BUILD_NUMBER}<br/>" +
                "URL: ${env.BUILD_URL}<br/>",
            to: 'trainerreyaz@gmail.com',
            attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
        }
    }
}

Step 10 — Docker Image Build and Push
======================================

Goto Jenkins Dashboard → Manage Jenkins → Credentials
Kind = Username and Password
Scope = Global
username = trainerreyaz
password =
ID = docker
Desc = docker


sudo chmod 777 /var/run/docker.sock
systemctl daemon-reload
systemctl restart docker.service


pipeline{
    agent any
    tools{
        jdk 'jdk23'
        nodejs 'node23'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/ReyazShaik/devsecops-netflix.git'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=netflix \
                    -Dsonar.projectKey=netflix '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh "docker build --build-arg TMDB_V3_API_KEY=cacc35c61cd76805987aca08d540f24e -t netflix ."
                       sh "docker tag netflix trainerreyaz/netflix:latest "
                       sh "docker push trainerreyaz/netflix:latest "
                    }
                }
            }
        }
        stage("TRIVY"){
            steps{
                sh "trivy image trainerreyaz/netflix:latest > trivyimage.txt"
            }
        }
       stage('Deploy to container'){
            steps{
                sh 'docker run -d --name netflix -p 8081:80 trainerreyaz/netflix:latest'
            }
        }
    }
    post {
     always {
        emailext attachLog: true,
            subject: "'${currentBuild.result}'",
            body: "Project: ${env.JOB_NAME}<br/>" +
                "Build Number: ${env.BUILD_NUMBER}<br/>" +
                "URL: ${env.BUILD_URL}<br/>",
            to: 'trainerreyaz@gmail.com',
            attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
        }
    }
}

http://jenkinsip:8081

Step 11 — Kuberenetes Setup 
===========================

Let’s Update the kubeconfig
============================

Go to Jenkins instance and enter the below command

aws eks update-kubeconfig --name EKS_CLUSTER --region ap-south-1

cat .kube/config

copy the entire content and save it as secret.txt in local machine

kubectl get nodes

Install Kubernetes Plugin
----------------------

Kubernetes Credentials
Kubernetes Client API
Kubernetes
Kubernetes CLI

goto manage Jenkins –> manage credentials –> Click on Jenkins global –> add credentials

Kind= SEcret File
choose = secret.txt
ID: k8s
desc : k8s



Now ready for final Pipeline
=============================

pipeline{
    agent any
    tools{
        jdk 'jdk23'
        nodejs 'node23'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/ReyazShaik/devsecops-netflix.git'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=netflix \
                    -Dsonar.projectKey=netflix '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh "docker build --build-arg TMDB_V3_API_KEY=cacc35c61cd76805987aca08d540f24e -t netflix ."
                       sh "docker tag netflix trainerreyaz/netflix:latest "
                       sh "docker push trainerreyaz/netflix:latest "
                    }
                }
            }
        }
        stage("TRIVY"){
            steps{
                sh "trivy image trainerreyaz/netflix:latest > trivyimage.txt"
            }
        }
       stage('Deploy to container'){
            steps{
                sh 'docker run -d --name netflix -p 3001:80 trainerreyaz/netflix:latest'
            }
        }
       stage('Deploy to kubernetes'){
            steps{
                script{
                    dir('Kubernetes') {
                        withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                                sh 'kubectl apply -f deployment.yml'
                                sh 'kubectl apply -f service.yml'
                        }
                    }
                }
            }
        }

    }
}


Note: in GitHub change the repo of yuours under Kubernetes deployment.yml

Note: if any error that container already exits

docker ps -a
docker stop contid
docker rm contd

and rerun the pipeline

kubectl get all
kubectl get svc #use anyone

