pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/swetabh65/JenkinsDryRunWithFlask.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask-app-container flask-app || true'
            }
        }
    }
}
