pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/MariamMoumen1/skin-cancer-detection-projet-main.git'
            }
        }
        stage('Build Frontend') {
            steps {
                bat 'docker build -f Dockerfile.frontend -t skin-cancer-frontend:latest .'
            }
        }
        stage('Build Backend') {
            steps {
                bat 'docker build -f Dockerfile.backend -t skin-cancer-backend:latest .'
            }
        }
        stage('Deploy MySQL') {
            steps {
                bat 'kubectl apply -f k8s/mysql-deployment.yaml'
                bat 'kubectl apply -f k8s/mysql-service.yaml'
            }
        }
        stage('Deploy Backend') {
            steps {
                bat 'kubectl apply -f k8s/backend-deployment.yaml'
                bat 'kubectl apply -f k8s/backend-service.yaml'
            }
        }
        stage('Deploy Frontend') {
            steps {
                bat 'kubectl apply -f k8s/frontend-deployment.yaml'
                bat 'kubectl apply -f k8s/frontend-service.yaml'
            }
        }
        stage('Verify Deployment') {
            steps {
                bat 'kubectl rollout status deployment/frontend'
                bat 'kubectl rollout status deployment/backend'
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }
}
