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
                sh 'docker build -t gowthamps03/trend-app:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                      echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                      docker push gowthamps03/trend-app:latest
                    '''
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh 'kubectl rollout restart deployment trend-app'
            }
        }
    }
}
