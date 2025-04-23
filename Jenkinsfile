pipeline {
    agent any

    environment {
        IMAGE_NAME = "webpage"
        IMAGE_TAG = "${env.BUILD_ID}"
        PORT = "8096"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    docker.image("${IMAGE_NAME}:${IMAGE_TAG}")
                          .run("-d -p ${PORT}:80 --name ${IMAGE_NAME}_${IMAGE_TAG}")
                }
            }
        }
    }

    post {
        success {
            echo "Deployment successful! Access at: http://<EC2_PUBLIC_IP>:${PORT}"
        }
        failure {
            echo "Deployment failed. Check logs above."
        }
    }
}
