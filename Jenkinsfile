pipeline {
    agent any

    environment {
        IMAGE_NAME = 'ahosan_jenkins_project_image'
        CONTAINER_NAME = 'ahosan_jenkins_project_container'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/MdAhosanHabib/ahosan_jenkins_project.git']])
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile from the repository
                    sh """
                    docker build -t ${IMAGE_NAME}:latest .
                    """
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container with the same name
                    sh """
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                    """
                    // Run the Docker container
                    sh """
                    docker run -d --name ${CONTAINER_NAME} -p 8181:80 ${IMAGE_NAME}:latest
                    """
                }
            }
        }
    }
}

