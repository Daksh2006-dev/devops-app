pipeline {
    agent any

    environment {
        EC2_IP = "54.225.5.230"
        APP_NAME = "devops-app"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Daksh2006-dev/devops-app.git',
                    branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t devops-app .
                '''
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(credentials: ['ec2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@54.225.5.230 "
                        docker rm -f devops-app || true
                        docker run -d -p 3000:3000 --name devops-app devops-app
                    "
                    '''
                }
            }
        }
    }
}
