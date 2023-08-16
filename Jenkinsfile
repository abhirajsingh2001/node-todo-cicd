pipeline {
    agent { label "Agent1" }
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/abhirajsingh2001/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t node-todo-app-cicd:v1"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                 sh "docker tag node-app-cicd:v1 ${env.dockerHubUser}/node-todo-app-cicd:v1"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/node-todo-app-cicd:v1"
                
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                sh echo "Code Deployed"
            }
        }
    }
}
