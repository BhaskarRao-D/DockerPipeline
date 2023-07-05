pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-bhaskarraodamuluri')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/BhaskarRao-D/DockerPipeline.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t bhaskarraodamuluri/nginx1:7 .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push bhaskarraodamuluri/nginx1:7'
            }
        }
        stage('pull image') {
            steps{
                sh 'docker pull bhaskarraodamuluri/nginx1:7'
            }
        }
      stage('run image') {
            steps{
                sh 'docker run -d -p 88:80 bhaskarraodamuluri/nginx1:7'
            }
        }   
}
post {
        always {
            sh 'docker logout'
        }
    }
}

