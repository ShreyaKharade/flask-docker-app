pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'SHREYA/flask-docker-app'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Flask application...'
                bat 'python --version'
                bat 'python -m py_compile app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo 'Docker image will be pushed to Docker Hub.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage completed.'
            }
        }
    }
}