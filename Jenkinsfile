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
                sh 'docker build -t poc8-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop poc8-app || true
                docker rm poc8-app || true
                docker run -d -p 3001:3000 --name poc8-app poc8-app
                '''
            }
        }
    }
}
