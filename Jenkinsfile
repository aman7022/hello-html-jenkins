pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials' // Use the credential ID you set earlier
        DOCKER_IMAGE_NAME = 'aman585/hello-html' // Replace with your Docker Hub repository name
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build("hello-html")
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                        sh "docker tag hello-html $DOCKER_IMAGE_NAME:latest"
                        sh "docker push $DOCKER_IMAGE_NAME:latest"
                    }
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8081:80 hello-html'
            }
        }
    }
}
