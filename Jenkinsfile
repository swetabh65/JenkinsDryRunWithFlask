pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'flask-app'
        CONTAINER_NAME = 'flask-app-container'
        PORT = '5000'
    }

    stages {
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
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    sh "docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
                }
            }
        }
    }
}
