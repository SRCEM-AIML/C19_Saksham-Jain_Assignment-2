pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'sakshamjain1712/studentproject'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/SRCEM-AIML/C19_Saksham-Jain_Assignment-2.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_HUB_REPO .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub-credentials', variable: 'DOCKER_HUB_PASS')]) {
                    sh 'echo $DOCKER_HUB_PASS | docker login -u YOUR_DOCKERHUB_USERNAME --password-stdin'
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push $DOCKER_HUB_REPO'
            }
        }
    }
}
