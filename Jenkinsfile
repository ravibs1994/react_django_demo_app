pipeline {
    agent any
    stages{
        stage('code pull'){
            steps{
                git url: "https://github.com/ravibs1994/react_django_demo_app.git", branch: "main"
            }
        }
        stage('Code build'){
           steps{
                sh 'docker build -t reactdjangoapp .'
            }
        }
        stage('push Docker image on Docker hub'){
            steps{
                echo 'pushing image on to docker hub'
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag reactdjangoapp ${env.dockerHubUser}/pipeline:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/pipeline:latest" 
                }
            }
        }
        stage('Deploy the container'){
            steps{
                sh 'docker run -d -p 8001:8001 ravindrahub/pipeline:latest'
            }
                
        }
        
     
    }
}
