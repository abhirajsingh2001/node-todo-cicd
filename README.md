# Jenkins Code Build and Deployment Automation

This repository outlines how to use Jenkins to automate the Code Build and Deployment processes, including creating Docker Images and deploying them as Docker containers.

## Prerequisites

Before getting started, make sure you have the following:

- Jenkins installed and configured.
- Docker installed on the target machine.
- Access to Docker Hub or your preferred container registry.

## Getting Started

To start using Jenkins for Code Build and Deployment Automation, follow these steps:

1. Clone this repository to your local machine or Jenkins server.
   ```groovy
     stage('Clode cloned'){
            steps{
                echo "Cloning the code from VCS Reposistory"
                git url: "https://github.com/abhirajsingh2001/node-todo-cicd.git", branch: "master"
                echo "Code Cloned"
            }
        }
   ```
   
2. Set up Jenkins according to your project's requirements.

3. Configure Jenkins jobs for Code Build, Docker Image Creation, and Deployment as Docker containers.
   ```groovy
   stage('Code Build'){
            steps{
                echo "Building the code"
                sh "docker build -t node-todo-cicd ."
                echo "Code Build"
            }
        }
         stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo "Code Deployed"
            }
        }
   ```
4. Customize the Jenkins pipeline or scripts to suit your specific project needs. In my case the pipleine looks like:
   ```groovy
        pipeline{
          agent any
          stages{
              stage('Clode cloned'){
                  steps{
                      echo "Cloning the code from VCS Reposistory"
                      git url: "https://github.com/abhirajsingh2001/node-todo-cicd.git", branch: "master"
                      echo "Code Cloned"
                  }
              }
              stage('Code Build'){
                  steps{
                      echo "Building the code"
                      sh "docker build -t node-todo-cicd ."
                      echo "Code Build"
                  }
              }
               stage("Deploy"){
                  steps{
                      sh "docker-compose down && docker-compose up -d"
                      echo "Code Deployed"
                  }
              }
            }
         }
   ```

6. Execute the Jenkins pipeline or jobs to automate your Code Build and Deployment processes.
   As we have deployed our application using docker you can check that your application is running or not, you use `docker ps` it will list all the running containers in your sytem. There the port number of the 
   application would be displayed. Open your browser type `http://system_ip:port_nubmer`.
