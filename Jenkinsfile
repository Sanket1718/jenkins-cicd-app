pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/<Sanket1718>/jenkins-cicd-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-cicd-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f myapp || true
                docker run -d -p 3000:3000 --name myapp jenkins-cicd-app
                '''
            }
        }
    }
}
