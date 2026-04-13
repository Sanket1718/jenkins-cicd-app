pipeline {
    agent any

    environment {
        AWS_ACCOUNT_ID = "142517507111"
        REGION = "ap-south-1"
        REPO = "jenkins-cicd-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-cicd-app .'
            }
        }

        stage('Tag Image') {
            steps {
                sh """
                docker tag jenkins-cicd-app:latest ${AWS_ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/${REPO}:latest
                """
            }
        }

        stage('Login to ECR') {
            steps {
                sh """
                aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com
                """
            }
        }

        stage('Push to ECR') {
            steps {
                sh """
                docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/${REPO}:latest
                """
            }
        }
    }
}
