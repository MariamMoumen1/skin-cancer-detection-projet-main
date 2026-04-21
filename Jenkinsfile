pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/MariamMoumen1/skin-cancer-detection-projet-main.git'
            }
        }
        stage('Build Frontend') {
            steps {
                sh 'docker build -f Dockerfile.frontend -t skin-cancer-frontend:latest .'
            }
        }
        stage('Build Backend') {
            steps {
                sh 'docker build -f Dockerfile.backend -t skin-cancer-backend:latest .'
            }
        }
        stage('Deploy MySQL') {
            steps {
                sh 'kubectl apply -f k8s/mysql-deployment.yaml'
                sh 'kubectl apply -f k8s/mysql-service.yaml'
            }
        }
        stage('Deploy Backend') {
            steps {
                sh 'kubectl apply -f k8s/backend-deployment.yaml'
                sh 'kubectl apply -f k8s/backend-service.yaml'
            }
        }
        stage('Deploy Frontend') {
            steps {
                sh 'kubectl apply -f k8s/frontend-deployment.yaml'
                sh 'kubectl apply -f k8s/frontend-service.yaml'
            }
        }
        stage('Verify Deployment') {
            steps {
                sh 'kubectl rollout status deployment/frontend'
                sh 'kubectl rollout status deployment/backend'
                sh 'kubectl get pods'
                sh 'kubectl get services'
            }
        }
    }
}
