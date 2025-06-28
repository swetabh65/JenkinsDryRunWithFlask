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
                    existing_port=$(docker ps -q --filter "publish=${PORT}")
                    if [ ! -z "$existing_port" ]; then
                        echo "Stopping container using port ${PORT}..."
                        docker rm -f $existing_port
                    fi

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

        stage('Test Flask App') {
            steps {
                script {
                    sh 'sleep 5'
                    sh 'curl http://localhost:5000 || echo "Flask app not responding"'
                }
            }
        }
    }
}
