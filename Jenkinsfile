pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials') // Your Docker Hub credentials
        DOCKER_IMAGE = 'kubeakshay111/flightbook' // Replace with your image name
        IMAGE_TAG = 'latest' // or use BUILD_NUMBER for unique tags
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from your repository
                git branch: 'FlightBook', url: 'https://github.com/akshaykm111/CICD-Docker-K8s.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh "docker build -t ${DOCKER_IMAGE}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push Docker image to Docker Hub
                    sh "docker push ${DOCKER_IMAGE}:${IMAGE_TAG}"
                }
            }
        }
    }

    post {
        always {
            script {
                // Clean up the workspace
                sh "docker rmi ${DOCKER_IMAGE}:${IMAGE_TAG}"
            }
        }
    }
}
