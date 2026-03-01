pipeline {
    agent any

    environment {
        IMAGE_NAME = "Nodejs-app"
        DOCKER_REGISTRY = "venky-217"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm install'
                sh 'npm test'
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry("https://index.docker.io/v1/", 'dockerhub-credentials') {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment step - customize for your environment"
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
