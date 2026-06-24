pipeline {
    agent any

    environment {
        IMAGE_NAME = "ibadzm/ibadazam-cicd-project"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
            }
        }

        stage('Docker Login Test') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub',
            usernameVariable: 'USERNAME',
            passwordVariable: 'PASSWORD'
        )]) {
            bat '''
            echo Username=%USERNAME%
            powershell -command "$env:PASSWORD.Length"
            '''
        }
    }
}

        stage('Push Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:%BUILD_NUMBER%'
            }
        }
    }
}
