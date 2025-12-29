pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Gowthamps2003/Trend.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t gowthamps2003/trend-app:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker push gowthamps2003/trend-app:latest'
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh 'kubectl rollout restart deployment trend-app'
            }
        }
    }
}
