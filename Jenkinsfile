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

        stage('Cleanup Port/Container') {
            steps {
                script {
                    // Stop and remove existing container using the same port (if any)
                    sh '''
                    existing_container=$(docker ps -q --filter "publish=${PORT}")
                    if [ ! -z "$existing_container" ]; then
                        echo "Stopping container using port ${PORT}..."
                        docker rm -f $existing_container
                    fi
                    '''
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
                }
            }
        }
    }
}
