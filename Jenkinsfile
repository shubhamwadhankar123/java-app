pipeline {
    agent any

    environment {
        IMAGE_NAME = 'shubhamwadhankar2103/javakubernetes:02'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/shubhamwadhankar123/java_app.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-credentials', url: '']) {
                    bat "docker push %IMAGE_NAME%"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f kubernetes/deployment.yml'
                bat 'kubectl apply -f kubernetes/service.yml'
            }
        }
    }
}
