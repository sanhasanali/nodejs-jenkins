pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dockerhubusername/nodejs-jenkins'
        TAG = 'latest'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials-id'  // Pastikan ini adalah ID kredensial yang benar
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
                    // Pastikan Docker build berhasil
                    docker.build("${DOCKER_IMAGE}:${TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Pastikan kredensial Docker benar
                    docker.withRegistry('https://index.docker.io/v1/', REGISTRY_CREDENTIALS) {
                        docker.image("${DOCKER_IMAGE}:${TAG}").push()  // Menggunakan 'docker.image' untuk push image
                    }
                }
            }
        }
    }
}
