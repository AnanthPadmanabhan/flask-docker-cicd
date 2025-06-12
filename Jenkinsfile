pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flask-docker-cicd'
        DOCKERHUB_USER = 'ananthpadmanabhan'
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(IMAGE_NAME)
                }
            }
        }

        stage('Test Container') {
            steps {
                bat 'docker run --rm -d -p 5000:5000 --name test-app flask-docker-cicd'
                bat 'timeout /t 5 /nobreak'
                bat 'curl -f http://localhost:5000'
                bat 'docker stop test-app'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    bat "docker tag ${IMAGE_NAME} ${DOCKERHUB_USER}/${IMAGE_NAME}:latest"
                    bat "docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:latest"
                }
            }
        }
    }
}