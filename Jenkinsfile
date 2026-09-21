pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                bat 'javac Main.java'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t java-docker-cicd:%BUILD_NUMBER% .'
            }
        }

        stage('Docker Image Check') {
            steps {
                bat 'docker images'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker run -d --name java-cicd-container-%BUILD_NUMBER% -p 8083:8080 java-docker-cicd:%BUILD_NUMBER%'
            }
        }
    }
}