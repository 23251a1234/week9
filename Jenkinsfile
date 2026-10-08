pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t greeshma2005/mypythonflaskapp:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    bat 'echo %DOCKER_PASSWORD%| docker login --username %DOCKER_USER% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push greeshma2005/mypythonflaskapp:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get svc'
            }
        }
    }
}