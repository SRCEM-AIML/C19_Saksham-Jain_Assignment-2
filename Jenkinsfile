pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sakshamjain1712/studentproject'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/SRCEM-AIML/C19_Saksham-Jain_Assignment-2.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'dockerhub-credentials', url: 'https://index.docker.io/v1/']) {
                        sh 'docker push $DOCKER_IMAGE'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Stop any running container with the same name
                    sh 'docker stop studentproject || true && docker rm studentproject || true'

                    // Run the new container
                    sh 'docker run -d --name studentproject -p 9030:9400 $DOCKER_IMAGE'
                }
            }
        }
    }
}
