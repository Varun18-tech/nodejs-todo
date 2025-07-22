// Jenkinsfile
pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "my-nodejs-todo-app"
    }
    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code using SSH...'
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER} ."
            }
        }
        stage('Deploy To-Do App') {
            steps {
                sh "docker stop ${DOCKER_IMAGE_NAME} || true"
                sh "docker rm ${DOCKER_IMAGE_NAME} || true"
                sh "docker run -d --name ${DOCKER_IMAGE_NAME} -p 8081:3000 ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER}"
            }
        }
    }
    post {
        always {
            sh 'docker image prune -f'
        }
    }
}
