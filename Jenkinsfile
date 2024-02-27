pipeline {
    agent { label "dev" }
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/NancyR17/node-todo-cicd.git", branch: "master"
                echo 'code clone ho gaya'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app-test-new ."
                echo 'code build bhi ho gaya'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                echo 'image push ho gaya'
                }
              }
            }
        stage("deploy-deploy with docker-compose"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment ho gaya'
            }
        }
    }
}
