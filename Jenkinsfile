pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('Docker-Hub-Cred')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/BhaskarRao-D/DockerPipeline.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t champ98:nginx:latest .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push champ98/nginx:latest'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull champ98/nginx:latest'
            }
        }
      stage('run image') {
            steps{
                sh 'docker run -d -p 443:80 champ98/nginx:latest'
            }
        }   
}
post {
        always {
            sh 'docker logout'
        }
    }
}

