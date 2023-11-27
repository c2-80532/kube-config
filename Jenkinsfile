pipeline {
    agent any

    environment {
        // Define environment variables
        registryCredential = 'dockerhub-credentials'
        dockerImage = 'your-docker-image-name:latest'
        kubeConfig = credentials('kubeconfig-credentials-id')
    }

    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build and push Docker image
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                        def customImage = docker.build(dockerImage)
                        customImage.push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Deploy to Kubernetes
                    withKubeConfig([credentialsId: 'kubeconfig-credentials-id', serverUrl: 'https://your-kube-api-server']) {
                        sh 'kubectl apply -f your-replicaset.yaml'
                        sh 'kubectl apply -f new_service.yaml'
                    }
                }
            }
        }
    }
}


