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
bat 'minikube delete --all --purge'

// Start a new Minikube cluster with Docker driver
bat 'minikube start --driver=docker'

// Enable the Kubernetes Dashboard addon
bat 'minikube addons enable dashboard'

// Pull the necessary base image explicitly to avoid errors
bat 'docker pull gcr.io/k8s-minikube/kicbase:v0.0.45'

// Apply Kubernetes deployment and service configurations
bat 'kubectl apply -f my-kube1-deployment.yaml'
bat 'kubectl apply -f my-kube1-service.yaml'

// Check the status of the resources to ensure they are running
bat 'kubectl get all'

// Expose and launch the Kubernetes Dashboard
bat 'minikube dashboard --url'

// Deployment status message
echo 'Application deployed successfully. Access the dashboard via the displayed URL.'

                }
            }
        }
    }
}
