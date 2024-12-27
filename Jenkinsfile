pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t ci-cd-app .'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'docker run -d -p 3000:3000 --name ci-cd-app-container ci-cd-app'
                    sh 'curl -f http://localhost:3000 || exit 1'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'docker stop ci-cd-app-container || true && docker rm ci-cd-app-container || true'
                    sh 'docker run -d -p 3000:3000 --name ci-cd-app-container ci-cd-app'
                }
            }
        }
    }
}