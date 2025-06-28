pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'flask-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/swetabh65/JenkinsDryRunWithFlask.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop & remove if already running (to avoid duplicate errors)
                    sh 'docker rm -f flask-app-container || true'
                    sh "docker run -d -p 5000:5000 --name flask-app-container ${DOCKER_IMAGE}"
                }
            }
        }
    }
}
