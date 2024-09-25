pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        DOCKER_USERNAME = credentials('a4d018fb-620b-48b7-a2b3-940e89cec33a') 
        DOCKER_PASSWORD = credentials('a4d018fb-620b-48b7-a2b3-940e89cec33a')
    }

    stages {
        stage('Checkout code') {
            steps {
                checkout scm
            }
        }

        stage('Log in to DockerHub') {
            steps {
                script {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
            }
        }

        stage('Build and push Docker image') {
            steps {
                script {
                    def imageName = "${DOCKER_USERNAME}/linear-regression-app"
                    sh """
                        docker build -t ${imageName} .
                        docker tag ${imageName} ${imageName}:latest
                        docker push ${imageName}:latest
                    """
                }
            }
        }
    }
}