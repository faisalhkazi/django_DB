pipeline {
    agent any 
    
    stages{
            
        stage("code"){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/faisalhkazi/django_DB.git", branch:"main"
            }
        }
        stage("build"){
            steps{
                echo "Building the code"
                sh "docker build -t my-note-app ."
            }
        }
        stage("push to DockerHub"){
            steps{
                echo "Pushing to the dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
                
            }
        }
        stage("deploy"){
            steps{
                echo "Deploying"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
