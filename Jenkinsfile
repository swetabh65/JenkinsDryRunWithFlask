pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'flask-app'
        DOCKER_TAG = 'latest'
        DOCKER_USERNAME = 'swetabh65'
        CONTAINER_NAME = 'flask-app-container'
        PORT = '5000'
    }

    stages {
        stage('Docker Build') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Cleanup Previous Containers') {
            steps {
                script {
                    sh '''
                    existing_port=$(docker ps -q --filter "publish=5000")
                    if [ ! -z "$existing_port" ]; then
                        echo "Stopping container using port 5000..."
                        docker rm -f $existing_port
                    fi

                    existing_named=$(docker ps -aq --filter "name=flask-app-container")
                    if [ ! -z "$existing_named" ]; then
                        echo "Removing existing container named flask-app-container..."
