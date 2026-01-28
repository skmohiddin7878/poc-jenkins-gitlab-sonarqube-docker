pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t poc-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop poc-app || true
                docker rm poc-app || true
                docker run -d -p 3000:3000 --name poc-app poc-app
                '''
            }
        }
    }
}

