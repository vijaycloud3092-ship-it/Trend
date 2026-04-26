pipeline {
    agent any

    environment {
        IMAGE_NAME = "ojasvijay/trend-app"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch:'main',url: 'https://github.com/vijaycloud3092-ship-it/Trend.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }
}
