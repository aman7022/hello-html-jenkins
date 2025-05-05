pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build("hello-html")
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:80 hello-html'
            }
        }
    }
}
