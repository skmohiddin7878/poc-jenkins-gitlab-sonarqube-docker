pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://gitlab.com/YOUR_USERNAME/poc-jenkins-gitlab-sonarqube-docker.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t poc-app .'
            }
        }

        stage('Deploy Application') {
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

