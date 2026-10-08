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
                bat 'docker login -u greeshma2005'
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