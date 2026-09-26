pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'shreyakharade/flask-docker-app'
        DOCKER_EXE = 'C:\\Users\\Asus\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
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

        stage('Check Docker') {
            steps {
                bat '"%DOCKER_EXE%" --version'
                bat '"%DOCKER_EXE%" info'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"%DOCKER_EXE%" build -t "%DOCKER_IMAGE%:%BUILD_NUMBER%" .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    bat '"%DOCKER_EXE%" login -u "%DOCKER_USERNAME%" -p "%DOCKER_PASSWORD%"'
                    bat '"%DOCKER_EXE%" push "%DOCKER_IMAGE%:%BUILD_NUMBER%"'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage completed successfully.'
            }
        }
    }
}