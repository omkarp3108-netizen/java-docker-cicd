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
                sh 'javac Main.java'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t java-docker-cicd:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Image Check') {
            steps {
                sh 'docker images'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d --name java-cicd-container-${BUILD_NUMBER} -p 8083:8080 java-docker-cicd:${BUILD_NUMBER}'
            }
        }
    }
}