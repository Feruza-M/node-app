pipeline {
    agent any

    environment {
        DOCKERHUB_USER = credentials('dockerhub-user')
        DOCKERHUB_PASS = credentials('dockerhub-pass')
        IMAGE_NAME = "docferuza2024/node-app"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'git@github.com:Feruza-M/node-app.git', branch: 'main'
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Push Image') {
            steps {
                sh "docker login -u '$DOCKERHUB_USER' -p '$DOCKERHUB_PASS'"
                sh "docker push ${IMAGE_NAME}:latest"
            }
        }

        stage('Deploy') {
            steps {
                sh "docker rm -f node-app || true"
                sh "docker run -d --name node-app -p 3001:3000 ${IMAGE_NAME}:latest"
            }
        }
    }
}
