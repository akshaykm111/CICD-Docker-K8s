pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKER_IMAGE = 'kubeakshay111/flightbook'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'FlightBook', url: 'https://github.com/akshaykm111/CICD-Docker-K8s.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:V${BUILD_NUMBER} ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${DOCKER_IMAGE}:V${BUILD_NUMBER}"
                }
            }
        }
    }

    post {
        always {
            script {
                // Clean up the workspace
                sh "docker rmi ${DOCKER_IMAGE}:V${BUILD_NUMBER}"
            }
        }
    }
}
