pipeline {
    agent {label 'dev-agent'}
    
    stages{
        stage('CODE CLONE'){
            steps{
                git url: "https://github.com/Kunalnaikodi/node-todo-cicd.git", branch: "master"
            }
        }
        
        
        
        stage('Code build and Test'){
            steps{
                sh "docker build . -t kunal26041999/node-todo-cicd:latest"
            }
        }
        
          stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
            
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push kunal26041999/node-todo-cicd:latest"

                }
            }
        }
      
        
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
