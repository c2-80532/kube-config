pipeline {
    agent any

    environment {
        // Define environment variables
        registryCredential = 'dockerhub-credentials'
        dockerImage = 'shubhamchau/assign8q3:1.1'
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
                    withKubeConfig([credentialsId: 'kubeconfig-credentials-id', serverUrl: 'https://192.168.49.2:8443']) {
                        sh 'kubectl apply -f kubeserv.yml'
                    }
                }
            }
        }
    }
}


