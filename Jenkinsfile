pipeline {
    agent any

    environment {
        EC2_IP = "54.225.5.230"
        APP_NAME = "devops-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Daksh2006-dev/devops-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-app .'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(credentials: ['ec2-ssh-key']) {
                    sh """
                    ssh -o StrictHostKeyChecking=no ubuntu@${EC2_IP} '
                        docker rm -f devops-app || true
                        docker pull devops-app || true
                        docker run -d -p 3000:3000 --name devops-app devops-app
                    '
                    """
                }
            }
        }
    }
}
