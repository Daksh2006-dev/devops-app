pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                echo 'Cloning repository'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f devops-app || true
                docker run -d -p 3000:3000 --name devops-app devops-app
                '''
            }
        }
    }
}
