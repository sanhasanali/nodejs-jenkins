pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dockerhubusername/nodejs-jenkins'
        TAG = 'latest'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials-id'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sanhasanali/nodejs-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', REGISTRY_CREDENTIALS) {
                        docker.image("${DOCKER_IMAGE}:${TAG}").push()
                    }
                }
            }
        }
    }
}
