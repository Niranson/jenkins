pipeline {
    agent any

    environment {
        DOCKER_USER = "your-dockerhub-username"
        IMAGE_NAME = "myapp"
    }

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKER_USER/$IMAGE_NAME:latest .'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push $DOCKER_USER/$IMAGE_NAME:latest'
                }
            }
        }
    }
}
