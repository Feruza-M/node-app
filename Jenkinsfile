pipeline {
    agent any

    environment {
        DOCKERHUB_USER = credentials('dockerhub-username') 
        DOCKERHUB_PASS = credentials('dockerhub-password') 
        IMAGE_NAME = "docferuza2024/node-app"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/AnastasiyaGapochkina01/node-app.git'
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Push Image') {
            steps {
                sh "echo ${DOCKERHUB_PASS} | docker login -u ${DOCKERHUB_USER} --password-stdin"
                sh "docker push ${IMAGE_NAME}:latest"
            }
        }

        stage('Deploy') {
            steps {
                sh "docker rm -f node-app || true"
                sh "docker run -d --name node-app -p 3000:3000 ${IMAGE_NAME}:latest"
            }
        }
    }
}
