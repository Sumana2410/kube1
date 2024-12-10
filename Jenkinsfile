pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                script {
                    // Build and push Docker image
                    bat 'docker build -t w9-dd-app:latest .'
                    bat 'docker tag w9-dd-app:latest pnvsumanasree/w9-dh-app:latest'
                    bat 'docker push pnvsumanasree/w9-dh-app:latest'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Delete and start Minikube cluster
                    // Delete existing Minikube cluster (if exists)
                     bat 'minikube delete'
                    bat 'minikube start'

                    bat 'minikube addons enable dashboard'

                    bat 'kubectl apply -f my-kube1-deployment.yaml'
                    bat 'kubectl apply -f my-kube1-service.yaml'
                    bat 'minikube dashboard'

                }
            }
        }
    }
}
