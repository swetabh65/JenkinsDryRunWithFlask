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

        stage('Cleanup Previous Containers') {
            steps {
                script {
                    sh '''
                    # Stop container using port 5000
                    existing_port=$(docker ps -q --filter "publish=${PORT}")
                    if [ ! -z "$existing_port" ]; then
                        echo "Stopping container using port ${PORT}..."
                        docker rm -f $existing_port
                    fi

                    # Remove container with same name if it exists
                    existing_named=$(docker ps -aq --filter "name=${CONTAINER_NAME}")
                    if [ ! -z "$existing_named" ]; then
                        echo "Removing existing container named ${CONTAINER_NAME}..."
                        docker rm -f $existing_named
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
